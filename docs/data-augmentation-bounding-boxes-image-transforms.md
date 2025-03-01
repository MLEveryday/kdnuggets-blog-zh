# 边框数据增强：重新思考用于目标检测的图像变换

> 原文：[https://www.kdnuggets.com/2018/09/data-augmentation-bounding-boxes-image-transforms.html](https://www.kdnuggets.com/2018/09/data-augmentation-bounding-boxes-image-transforms.html)

![c](../Images/3d9c022da2d331bb56691a9617b91b90.png) [评论](/2018/09/data-augmentation-object-detection-rethinking-image-transforms-bounding-boxes.html?page=2#comments)

**由[Ayoosh Kathuria](https://www.linkedin.com/in/ayoosh-kathuria-44a319132/)，研究实习生**

在获得深度学习任务的良好表现时，数据越多越好。然而，我们可能只有有限的数据。数据增强是一种应对数据短缺的方法，通过人工扩展数据集。事实上，这种技术已经证明非常成功，已成为深度学习系统的基本组成部分。

### 数据增强为何有效？

理解数据增强为何有效的一个非常直接的方式是将其视为一种人工扩展数据集的方法。正如深度学习应用中的情况一样，数据越多越好。

另一个理解数据增强为何如此有效的方法是将其视为对数据集添加噪声。这在在线数据增强的情况下尤为明显，即每次将数据样本馈送到训练循环中时都会随机增强。

![](../Images/6e61e5d199221bf1c5b843f8f13cfd0a.png)

*左侧*：原始图像，*右侧*：增强图像。

每次神经网络看到相同的图像时，由于施加了随机的数据增强，图像会有些许不同。这种差异可以看作是每次对数据样本添加的噪声，这种噪声迫使神经网络学习泛化特征，而不是对数据集进行过拟合。

### GitHub 仓库

本文及整个增强库的内容可以在以下GitHub仓库中找到。

**[https://github.com/Paperspace/DataAugmentationForObjectDetection](https://github.com/Paperspace/DataAugmentationForObjectDetection)**

### 文档

该项目的文档可以通过在浏览器中打开`docs/build/html/index.html`或访问这个[链接](https://augmentationlib.paperspace.com/)找到。

本系列共有4部分。

+   [第1部分：基本设计与水平翻转](https://blog.paperspace.com/data-augmentation-for-bounding-boxes/)

+   [第2部分：缩放与平移](https://blog.paperspace.com/data-augmentation-bounding-boxes-scaling-translation/)

+   [第3部分：旋转与剪切](https://blog.paperspace.com/data-augmentation-for-object-detection-rotation-and-shearing/)

+   [第4部分：将增强方法融入输入管道](https://blog.paperspace.com/data-augmentation-for-object-detection-building-input-pipelines/)

### 边框对象检测

现在，许多深度学习库，如torchvision、keras以及GitHub上的专用库，提供了分类训练任务的数据增强。然而，对对象检测任务的数据增强支持仍然缺失。例如，用于分类任务的图像水平翻转增强将类似于上面显示的样子。

然而，对对象检测任务执行相同的增强也需要你更新边界框。例如，如下图所示。

![](../Images/a2ac179bf8f51bd5d52db37137d3d7af.png)

水平翻转时的边界框变化

正是这种数据增强，或者说是数据增强技术**需要我们更新边界框**的检测等效方法，是我们将在这些文章中探讨的。具体来说，这里是我们将涵盖的增强列表。

1.  水平翻转（如上所示）

1.  缩放和平移

    ![](../Images/4c467e8b4a1b1c8650f02016acda5a03.png)

1.  旋转

    ![](../Images/8e8f2d946410acaa88cc23226bf65b4a.png)

1.  剪切

    ![](../Images/44408836b2cf9d23de012bdfb7b76798.png)

1.  神经网络输入的缩放

### 技术细节

我们的小型数据增强库将基于**Numpy**和**OpenCV**。

我们将把增强定义为类，其实例可以被调用以执行增强。我们将定义一种统一的方法来定义这些类，以便你也可以编写自己的数据增强。

我们还将定义一个数据增强，它本身不做任何事，但结合数据增强，以便它们可以在**序列**中应用。

对于每种数据增强，我们将定义其两个变体，一个是**随机**的，一个是**确定性**的。在随机变体中，增强是随机发生的，而在确定性变体中，增强的参数（如旋转角度）保持不变。

### 示例数据增强：水平翻转

本文将概述编写增强的总体方法。我们还会介绍一些实用函数，帮助我们可视化检测和其他内容。让我们开始吧。

### 注释存储格式

对于每张图片，我们在一个numpy数组中存储边界框注释，数组具有*N*行和5列。这里，*N*表示图片中的对象数量，而五列表示：

1.  左上角的*x*坐标

1.  左上角的*y*坐标

1.  右下角的*x*坐标

1.  右下角的*y*坐标

1.  对象的类别

![](../Images/7464457fea0838197eabd08fe7f60a00.png)

存储边界框注释的格式

我知道很多数据集和注释工具以其他格式存储注释，因此，我将把它留给你，将数据注释存储的格式转换为上述描述的格式。

是的，为了演示目的，我们将使用以下图片，展示莱昂内尔·梅西对尼日利亚打进的精彩进球。

### 文件组织

我们将代码保存在两个文件中，`data_aug.py`和`bbox_util.py`。第一个文件包含数据增强的代码，而第二个文件包含辅助函数的代码。

这两个文件都将位于名为`data_aug`的文件夹中

假设你需要在训练循环中使用这些数据增强。我会让你找出如何提取图像并确保标注格式正确。

然而，为了简化操作，我们一次只使用一张图像。你可以轻松地将此代码放入循环中，或你的数据提取函数中以扩展功能。

克隆包含训练代码文件或需要进行数据增强的文件的 github 仓库。

```py
git clone https://github.com/Paperspace/DataAugmentationForObjectDetection
```

* * *

## 我们的前三大课程推荐

![](../Images/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业轨道

![](../Images/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](../Images/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌IT支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你组织的IT需求

* * *

### 更多相关话题

+   [边界框深度学习：视频标注的未来](https://www.kdnuggets.com/2022/07/bounding-box-deep-learning-future-video-annotation.html)

+   [IT员工扩充：AI如何改变软件开发行业](https://www.kdnuggets.com/2023/05/staff-augmentation-ai-changing-software-development-industry.html)

+   [语义向量搜索如何改变客户支持互动](https://www.kdnuggets.com/how-semantic-vector-search-transforms-customer-support-interactions)

+   [KDnuggets™ 新闻 22:n09, 3月2日：讲述伟大的数据故事：A…](https://www.kdnuggets.com/2022/n09.html)

+   [SQL与对象关系映射（ORM）之间的区别是什么？](https://www.kdnuggets.com/2022/02/difference-sql-object-relational-mapping-orm.html)

+   [数据科学中异常检测技术的初学者指南](https://www.kdnuggets.com/2023/05/beginner-guide-anomaly-detection-techniques-data-science.html)
��，其中 N 是对象的数量，每个框由具有 5 个属性的行表示；**即左上角坐标、右下角坐标以及对象的类别。**

+   每种数据增强被定义为一个类，其中`__init__`方法用于定义增强的参数，而`__call__`方法描述增强的实际逻辑。它接受两个参数，图像`img`和边界框注释`bboxes`，并返回转换后的值。

这就是本文的内容。在下一篇文章中，我们将处理`Scale`和`Translate`增强。这些不仅是更复杂的变换，因为涉及更多的参数（缩放和翻译因子），而且还带来了一些我们在`HorizontalFlip`变换中未曾遇到的挑战。例如，要决定在增强后如果部分框在图像之外时是否保留该框。

**简历：[Ayoosh Kathuria](https://www.linkedin.com/in/ayoosh-kathuria-44a319132/)** 目前在印度国防研究与发展组织实习，致力于提高颗粒视频中的目标检测精度。当他不在工作时，他要么在睡觉，要么在弹吉他演奏 Pink Floyd。你可以在 [LinkedIn](https://www.linkedin.com/in/ayoosh-kathuria-44a319132/) 上与他联系，或在 [GitHub](https://github.com/ayooshkathuria) 上查看他的更多工作。

[原文](https://blog.paperspace.com/data-augmentation-for-bounding-boxes/)。已获许可转载。

**相关：**

+   [如何从零开始在 PyTorch 中实现 YOLO (v3) 目标检测器：第 1 部分](/2018/05/implement-yolo-v3-object-detector-pytorch-part-1.html)

+   [使用 Tensorflow 对象检测 API 构建玩具检测器](/2018/02/building-toy-detector-tensorflow-object-detection-api.html)

+   [开始使用 PyTorch 第 1 部分：理解自动微分的工作原理](/2018/04/getting-started-pytorch-understanding-automatic-differentiation.html)

* * *

## 我们的三大课程推荐

![](../Images/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业生涯。

![](../Images/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](../Images/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织进行 IT

* * *

### 更多相关主题

+   [边界框深度学习：视频标注的未来](https://www.kdnuggets.com/2022/07/bounding-box-deep-learning-future-video-annotation.html)

+   [IT 人员增补：人工智能如何改变软件开发行业](https://www.kdnuggets.com/2023/05/staff-augmentation-ai-changing-software-development-industry.html)

+   [语义向量搜索如何改变客户支持互动](https://www.kdnuggets.com/how-semantic-vector-search-transforms-customer-support-interactions)

+   [KDnuggets™ 新闻 22:n09, 3月2日：讲述一个伟大的数据故事：A…](https://www.kdnuggets.com/2022/n09.html)

+   [SQL 和对象关系映射（ORM）之间有什么区别？](https://www.kdnuggets.com/2022/02/difference-sql-object-relational-mapping-orm.html)

+   [数据科学中的异常检测技术初学者指南](https://www.kdnuggets.com/2023/05/beginner-guide-anomaly-detection-techniques-data-science.html)
