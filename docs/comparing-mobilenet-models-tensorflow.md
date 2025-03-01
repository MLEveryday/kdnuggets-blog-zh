# 在 TensorFlow 中比较 MobileNet 模型

> 原文：[`www.kdnuggets.com/2019/03/comparing-mobilenet-models-tensorflow.html`](https://www.kdnuggets.com/2019/03/comparing-mobilenet-models-tensorflow.html)

![c](img/3d9c022da2d331bb56691a9617b91b90.png) 评论

**由 [Harshit Dwivedi](https://harshit.app/) 提供，Android 讲师**

![标题图像](img/b19415c11ab86d4e586a957be6c5ae05.png)

* * *

## 我们的前三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速开启网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升您的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持您的组织进行 IT 管理

* * *

近年来，神经网络和深度学习在 [自然语言处理](https://heartbeat.fritz.ai/the-7-nlp-techniques-that-will-change-how-you-communicate-in-the-future-part-i-f0114b2f0497)（NLP）和 [计算机视觉](https://heartbeat.fritz.ai/the-5-computer-vision-techniques-that-will-change-how-you-see-the-world-1ee19334354b) 领域取得了巨大进展。

虽然许多 [人脸](https://heartbeat.fritz.ai/building-a-real-time-face-detector-in-android-with-ml-kit-f930eb7b36d9)、[物体](https://heartbeat.fritz.ai/counting-items-in-real-time-on-android-with-fritz-object-detection-c450d6957448)、地标、徽标和 [文本识别](https://heartbeat.fritz.ai/choose-the-right-on-device-text-recognition-sdk-on-android-using-deltaml-9b4b3e409b6e) 和检测技术已提供给联网设备，但我们相信 [移动设备日益增长的计算能力](https://heartbeat.fritz.ai/hardware-acceleration-for-machine-learning-on-apple-and-android-f3e6ca85bda6) 可以使这些技术随时随地交到用户手中，无论是否有互联网连接。

然而，针对设备和嵌入式应用的计算机视觉面临许多挑战——模型必须在资源受限的环境中快速运行并保持高准确率，同时利用有限的计算能力、功耗和空间。

TensorFlow 提供了各种预训练模型，例如拖放模型，以识别约 1,000 种默认对象。

与其他类似模型（如 [Inception](https://github.com/tensorflow/models/tree/master/research/inception) 模型数据集）相比，[MobileNet](https://medium.com/@yu4u/why-mobilenet-and-its-variants-e-g-shufflenet-are-fast-1c7048b9618d) 在延迟、大小和准确性方面表现更好。在输出性能方面，完整模型存在显著的延迟。

然而，当模型可以部署到移动设备上进行实时离线检测时，这种权衡是可以接受的。

让我们看一个如何使用 MobileNet 的示例。我们将编写一个简单的分类器来识别图片中的 Pikachu。以下是显示 Pikachu 图片和不含 Pikachu 图片的示例：

![图](img/bf3576eec85638c94663edb9e2286300.png)

Pikachu![图](img/8ed1ecdd534c72ece76faecdf43ef50b.png)

不是 Pikachu，假设在 Pokémon Go 中没有 Pikachu 可收集……

### 构建数据集

要构建我们自己的分类器，我们需要有包含 Pikachu 和不包含 Pikachu 的图片的数据集。

让我们从每个数据库的 1,000 张图片开始。你可以在这里获取这样的图片：

[**CC 搜索**

*Creative Commons 许可证为作者、艺术家和教育工作者提供了一系列灵活的保护和自由。*

[search.creativecommons.org](https://search.creativecommons.org/)

接下来，让我们创建两个文件夹，命名为**pikachu**和**no-pikachu**，并将图片分别放入这些文件夹中。

另一个包含所有第一代 Pokémon 图片的实用数据集可以在这里找到：

[**Pokemon 第一代**

*必须训练全部！*

[www.kaggle.com](https://www.kaggle.com/thedagger/pokemon-generation-one)

现在我们有了一个图片文件夹，结构如下：

```py
/dataset/
/pikachu/[image1,..]
/no-pikachu/[image1,..]
```

**重训练图片**

现在我们可以开始标记我们的图片了。使用 TensorFlow，这项工作变得更容易。假设 TensorFlow 已经在训练机器上[安装](https://www.tensorflow.org/install/)，下载以下重训练脚本：

```py
curl https://github.com/tensorflow/hub/blob/master/examples/image_retraining/retrain.py
```

接下来，我们将使用此 Python 脚本重训练图片：

```py
python retrain.py \
--image_dir ~/MLmobileapps/Chapter5/dataset/ \
--learning_rate=0.0001 \
--testing_percentage=20 \
--validation_percentage=20 \
--train_batch_size=32 \
--validation_batch_size=-1 \
--eval_step_interval=100 \
--how_many_training_steps=1000 \
--flip_left_right=True \
--random_scale=30 \
--random_brightness=30 \
--architecture mobilenet_1.0_224 \
--output_graph=output_graph.pb \
--output_labels=output_labels.txt
```

> 注：如果将 `validation_batch_size` 设置为 -1，它将验证整个数据集。`learning_rate` = 0.0001 的效果很好。你可以调整并自己尝试。
> 
> 在 `architecture` 标志中，我们选择使用哪个版本的 MobileNet，版本包括 1.0、0.75、0.50 和 0.25。后缀数字 224 代表图像分辨率。你也可以指定 224、192、160 或 128。

### 从 GraphDef 到 TFLite 的模型转换

TOCO 转换器用于将 TensorFlow GraphDef 文件或 SavedModel 转换为 TFLite FlatBuffer 或图形可视化。

(TOCO 代表[**TensorFlow Lite 优化转换器**](https://www.tensorflow.org/lite/convert/))

我们需要通过命令行参数传递数据。在转换模型时可以传递一些命令行参数：

```py
--output_file OUTPUT_FILE
Filepath of the output tflite model.

--graph_def_file GRAPH_DEF_FILE
Filepath of input TensorFlow GraphDef.

--saved_model_dir
Filepath of directory containing the SavedModel.

--keras_model_file
Filepath of HDF5 file containing tf.Keras model.

--output_format {TFLITE,GRAPHVIZ_DOT}
Output file format.

--inference_type {FLOAT,QUANTIZED_UINT8}
Target data type in the output

--inference_input_type {FLOAT,QUANTIZED_UINT8}
Target data type of real-number input arrays.

--input_arrays INPUT_ARRAYS
Names of the input arrays, comma-separated.

--input_shapes INPUT_SHAPES
Shapes corresponding to --input_arrays, colon-separated.

--output_arrays OUTPUT_ARRAYS
Names of the output arrays, comma-separated.
```

我们现在可以使用 TOCO 工具将 TensorFlow 模型转换为[TensorFlow Lite](https://heartbeat.fritz.ai/how-tensorflow-lite-optimizes-neural-networks-for-mobile-machine-learning-e6ffa7f8ee12)模型：

```py
toco \
--graph_def_file=/tmp/output_graph.pb
--output_file=/tmp/retrained_model.tflite
--input_arrays=Mul
--output_arrays=final_result
--input_format=TENSORFLOW_GRAPHDEF
--output_format=TFLITE
--input_shape=1,${224},${224},3
--inference_type=FLOAT
--input_data_type=FLOAT
```

同样，我们可以在类似的应用中使用 MobileNet 模型；例如，在下一部分中，我们将讨论性别模型和情感模型。

### 性别模型

该模型使用[IMDB WIKI 数据集](https://data.vision.ee.ethz.ch/cvl/rrothe/imdb-wiki/)，包含超过 50 万张名人面孔。它使用 MobileNet_V1_224_0.5 版本的 MobileNet。

公开数据集中有数千张图像的情况非常罕见。该数据集基于大量名人面部图像集合构建。两个常见的来源是 IMDb 和维基百科。通过脚本从这两个来源的资料中检索了超过 10 万名名人的详细信息。

然后通过去除噪声（无关内容）来组织数据。所有没有时间戳的图像被删除，假设只有单张照片的图像更可能显示正确的出生日期细节。最终，共有来自 IMDb 的 20,284 名名人的 460,723 张面孔和来自维基百科的 62,328 张面孔，总计 523,051 张。

### 情感模型

该模型基于超过 100 万张图像的 AffectNet 模型。它使用了 MobileNet_V2_224_1.4 版本的 MobileNet。

数据模型项目的链接可以在这里找到：

[**AffectNet - Mohammad H. Mahoor, PhD**](http://mohammadmahoor.com/affectnet/)

*当前测试集尚未发布。我们计划在不久的将来组织一个 AffectNet 挑战赛，敬请期待…*

[mohammadmahoor.com](http://mohammadmahoor.com/affectnet/)

AffectNet 模型通过从互联网收集和标注超过 100 万张面部图像而建立。这些图像来自三个搜索引擎，使用了约 1250 个相关关键词，涵盖六种不同的语言。

在收集的图像中，一半的图像被手动标注了七种不同的面部表情（分类模型）以及情感的强度和唤醒度（维度模型）。

### MobileNet 版本对比

在上述两种模型中，使用了不同版本的 MobileNet 模型。MobileNet V2 主要是 V1 的更新版本，使其在性能方面更加高效和强大。

![图](img/555491ca9161425d40ad4aa667cf92bc.png)

注意：值越低越好

MACs 是[multiply-accumulate operations](https://www.semanticscholar.org/topic/Multiply%E2%80%93accumulate-operation/408575)，用于测量对单张 224×224 RGB 图像进行推断所需的计算次数。

从 MACs 的数量来看，V2 的速度应当几乎是 V1 的两倍。然而，这不仅仅关乎计算次数。在移动设备上，[内存访问](https://heartbeat.fritz.ai/profiling-your-app-with-android-studio-7accc268cb98)比计算要慢得多。V2 的参数数量只有 V1 的 80%，因此它比 V1 更优。

从结果来看，我们可以假设 V2 的速度几乎是 V1 模型的两倍。在内存访问受限的移动设备上，V2 的计算能力表现得非常好。

在准确性方面：

![图](img/7986e778d85c5164a94878ca5b376c05.png)

在这里，MobileNet V2 在性能上比 V1 稍好，虽然不一定显著。

### 结论

MobileNet 是一系列*以移动为优先*的计算机视觉模型，适用于[TensorFlow](https://www.tensorflow.org/)，旨在有效地最大化准确性，同时考虑到设备或嵌入式应用的有限资源。

MobileNets 是小型、低延迟、低功耗的模型，参数化以满足各种使用情况的资源限制。它们可以用于分类、检测、嵌入和分割，类似于其他流行的大规模模型，如 [Inception](https://arxiv.org/pdf/1602.07261.pdf)。

如果你想进一步探索和满足好奇心，可以在这里找到一堆预训练模型：

[**tensorflow/models**

*使用 TensorFlow 构建的模型和示例。通过创建账户来为 tensorflow/models 开发贡献力量…*

[github.com](https://github.com/tensorflow/models/blob/master/research/slim/nets/mobilenet_v1.md)

此外，这里有一篇博客文章概述了如何使用 MobileNets 和 TensorFlow Lite 构建一个真实的 Pokémon 分类器：

[**在 Android 中使用 TensorFlow Lite 和 Firebase 的 ML Kit 构建“宝可梦图鉴”**

[heartbeat.fritz.ai](https://heartbeat.fritz.ai/building-pok%C3%A9dex-in-android-using-tensorflow-lite-and-firebase-cc780848395)

*感谢阅读！如果你喜欢这个故事，请****点击 ***????*** 按钮******并分享****以帮助其他人找到它！欢迎在下面留下评论 *????*。有反馈？我们可以在*[*Twitter*](https://twitter.com/daggerdwivedi)*上联系。*

*如果你觉得这篇文章有趣，可以探索*[*移动应用的机器学习项目*](https://www.amazon.com/Machine-Learning-Projects-Mobile-Applications/dp/1788994590)*。由 ML 专家 Karthikeyan MG 撰写，*[*移动应用的机器学习项目*](https://www.packtpub.com/big-data-and-business-intelligence/machine-learning-projects-mobile-applications)* 介绍了 7 个实际的、真实世界的项目实施，这些项目将教你如何利用 TensorFlow Lite 和 Core ML 在跨平台移动操作系统上执行高效的机器学习。*

***想要开始构建令人惊叹的 Android 应用程序吗？查看我在 Coding Blocks 上的课程：***[`online.codingblocks.com/courses/android-app-training-online`](https://online.codingblocks.com/courses/android-app-training-online)

准备好进入代码世界了吗？查看 [Fritz 在 GitHub 上](https://github.com/fritzlabs)。你会找到流行的机器学习和深度学习模型的开源、适用于移动设备的实现，以及训练脚本、项目模板和用于构建自己的 ML 驱动的 iOS 和 Android 应用程序的工具。

加入我们在 [Slack](https://join.slack.com/t/heartbeat-by-fritz/shared_invite/enQtNTI4MDcxMzI1MzAwLWIyMjRmMGYxYjUwZmE3MzA0MWQ0NDk0YjA2NzE3M2FjM2Y5MjQxMWM2MmQ4ZTdjNjViYjM3NDE0OWQxOTBmZWI) 上的讨论，以获得技术问题的帮助，分享你正在做的工作，或与我们讨论移动开发和机器学习。关注我们的 [Twitter](https://twitter.com/fritzlabs) 和 [LinkedIn](https://www.linkedin.com/company/fritz-labs-inc/) 以获取移动机器学习世界的最新内容、新闻及更多信息。

感谢 [Austin Kodra](https://medium.com/@austin_32493?source=post_page)。

**简介： [Harshit Dwivedi](https://harshit.app/)** 对许多事物有*大致*的了解。他是 Coding Blocks 的 Android 教师，Fritz 的 Heartbeat 贡献作者，公共演讲者，以及天体物理学爱好者。

[原文](https://heartbeat.fritz.ai/exploring-the-mobilenet-models-in-tensorflow-d9d21774cdab)。经授权转载。

**相关：**

+   如何在计算机视觉中做一切

+   数据科学家/数据分析师的 10 款最佳移动应用

+   人工智能和机器学习的最新进展 - 带代码的论文亮点

### 更多相关主题

+   [PyTorch 还是 TensorFlow？比较流行的机器学习框架](https://www.kdnuggets.com/2022/02/packt-pytorch-tensorflow-comparing-popular-machine-learning-frameworks.html)

+   [比较线性回归与逻辑回归](https://www.kdnuggets.com/2022/11/comparing-linear-logistic-regression.html)

+   [比较自然语言处理技术：RNNs、Transformers、BERT](https://www.kdnuggets.com/comparing-natural-language-processing-techniques-rnns-transformers-bert)

+   [TensorFlow 在计算机视觉中的应用 - 转移学习简化](https://www.kdnuggets.com/2022/01/tensorflow-computer-vision-transfer-learning-made-easy.html)

+   [Tensorflow 的“Hello World”](https://www.kdnuggets.com/2022/05/hello-world-tensorflow.html)

+   [使用 Tensorflow 训练图像分类模型的指南](https://www.kdnuggets.com/2022/12/guide-train-image-classification-model-tensorflow.html)
