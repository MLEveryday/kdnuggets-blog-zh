# 敏捷数据标注：它是什么以及你为什么需要它

> 原文：[`www.kdnuggets.com/2021/08/agile-data-labeling.html`](https://www.kdnuggets.com/2021/08/agile-data-labeling.html)

评论

**由[Jennifer Prendki](https://www.linkedin.com/in/jennifer-prendki/)，Alectio 创始人兼首席执行官，机器学习企业家**。

敏捷这一概念在技术领域无疑非常流行，但这并不是你自然会将其与数据标注联系在一起的概念。这很容易理解：“敏捷”通常激发效率。然而，标注在 ML 圈子里几乎不会讨论而不引发一片沮丧的叹息声。

![](img/2a69714f0343bbdf8b13a8a22c67b775.png)

*图 1：敏捷宣言描述了一套软件开发人员认为能提高生产力的“规则”。*

要了解敏捷是如何被如此广泛采纳的，你需要追溯其起源。2001 年，一群 17 位软件工程师在犹他州的一个度假胜地聚集，头脑风暴如何让他们的行业变得更好。他们认为项目管理的方式不适当、效率低下且过于规范。因此，他们提出了敏捷宣言，这是一套他们认为可以提高软件工程团队生产力（以及理智水平！）的指南。敏捷宣言是对阻碍进展的缺乏过程的抗议。在许多方面，这正是数据标注所需要的。

![](img/aaabd13c338a086cf35121485f877684.png)

*图 2：深入探讨敏捷宣言及其核心原则。*

回到机器学习。毫无疑问，我们在过去几十年里在这一领域取得的进展是令人难以置信的。事实上，多数专家一致认为，这项技术的演变速度太快，超出了我们的法律和机构的跟上速度。（不信？只需想想 DeepFakes 对世界和平可能产生的严重后果）。尽管 AI 产品的爆炸性增长，ML 项目的成功归结为一件事：数据。如果你没有收集、存储、验证、清理或处理数据的手段，那么你的 ML 模型将永远只是一个遥远的梦想。即便是世界上最负盛名的 ML 公司之一[OpenAI 在意识到他们没有获得必要数据的手段后，决定关闭了一个部门](https://www.theregister.com/2021/07/18/in_brief_ai/)。

如果你认为只需找到一个开源数据集就可以开始工作，那就想错了：不仅相关的开源数据用例稀少，[这些数据集大多也存在令人惊讶的错误](https://www.technologyreview.com/2021/04/01/1021619/ai-data-errors-warp-machine-learning-progress?)，在生产中使用它们简直是极其不负责任的。

自然地，随着硬件越来越好且价格越来越便宜，收集自己的数据集应该不再是问题。不过，核心问题在于：这些数据不能直接使用，因为它们需要被标注。尽管看起来是这样，但这并不是一项简单的任务。

![](img/664090450f1cd450459a9f438f80fa81.png)

*图 3：对图像中的所有飞机进行标注，以便用于目标检测或目标分割用例，即使对经验丰富的专家来说，也可能需要花费一个多小时。想象一下需要为 50,000 张图片进行这种操作，并且在没有帮助的情况下保证标注的质量。*

数据标注是令人畏惧的。对于许多机器学习科学家来说，标注数据占据了他们工作量的极大部分。而且，虽然自己进行数据标注对大多数人来说并不是一项愉快的任务，但将这一过程外包给第三方可能会更加繁琐。

![](img/bb9599a27113baa93abadb3acf1f12cd.png)

*图 4：这是安德烈·卡帕提（Andrey Karpathy）在 2018 年 Train AI 大会上展示的一张幻灯片，讲述了他和他的团队在特斯拉进行数据准备的时间。*

想象一下，你需要向一个完全陌生且无法直接沟通的人解释什么是你认为的有毒推文、搜索查询的相关结果，或者图片中的行人。想象一下确保数百个人会以完全相同的方式理解你的指示，即使他们可能各自有不同的观点和背景，并且可能对你想要实现的目标一无所知。这正是将你的标注过程外包的意义所在。

![](img/11874c82953617f28992eac32e9cf50e.png)

*图 5：广告中的人应该被标记为人吗？*

这与敏捷开发有什么关系？如果你还没有猜到的话，机器学习科学家对标注的日益沮丧可能是我们重新思考如何完成工作的信号。是时候制定数据标注的敏捷宣言了。

软件开发的敏捷宣言本质上归结为一个基础概念：**反应性**。它表明一种固执的方法是行不通的。相反，软件工程师应该依靠反馈——来自客户、来自同事。他们应该准备好适应和从错误中学习，以确保能够实现最终目标。这很有趣，因为缺乏反馈和反应性正是团队害怕外包的原因。这也是标注任务常常需要花费大量时间并且可能花费公司数百万美元的主要原因。

成功的数据标注敏捷宣言应从相同的反应性原则开始，这一点在数据标注公司叙述中出奇地缺失。成功的训练数据准备涉及合作、反馈和纪律。

![](img/807342b142212398f8b15fe8f33a6c67.png)

*图 5：数据标注的敏捷宣言。*

### 1\. 结合多种方法/工具

**自动标注** 的概念，即利用机器学习模型生成“合成”标签，近年来变得越来越流行，为那些厌倦现状的人们带来了希望，但这只是简化数据标注的一种尝试。然而，现实是，没有单一的方法能够解决所有问题：例如，自动标注的核心是一个鸡与蛋的问题。这就是为什么**人机协作**标注的概念越来越受到关注。

尽管如此，那些尝试感觉上不够协调，并且对于经常难以看出这些新范式如何应用于自身挑战的公司几乎没有带来任何缓解。因此，行业需要更多关于现有工具的可见性和透明度（一个很好的初步尝试是 [TWIML 解决方案指南](https://twimlai.com/solutions/)，尽管它并非专门针对标注解决方案），以及这些工具之间的便捷集成，还有一个与机器学习生命周期其余部分自然集成的端到端标注工作流。

### 2\. 利用市场的优势

外包过程可能不是针对那些没有第三方能够提供令人满意结果的专业用例的选项。这是因为大多数标注公司依赖于众包或业务流程外包（BPO），这意味着他们的标注员并不是高技能的劳动力——他们无法为你标注脑癌 MRI 图像。幸运的是，一些初创公司现在专注于为特定领域提供专业服务。

无论你是否需要专家的帮助，找到合适的公司仍然很困难。大多数标注公司都提供全面服务，但最终都有各自的优缺点，客户往往只有在签署了一年合同后才发现这些优缺点。比较所有选项是找到你需要时现有最佳标注员的关键，并且应成为过程中的重要部分。

### 3\. 采取迭代的方法

数据标注的过程实际上出奇地没有反馈环路，尽管反馈在机器学习中至关重要。没有人会盲目地开发一个模型，但传统上就是这样生成标签的。采用爬行-走路-跑步的方法来调整和优化你的标注过程和数据集，显然是正确的方向。这就是为什么基于人机协作的范式，其中机器预标注而人类验证，显然是最佳选择。

更有前景的方法之一是倾听模型的提示，识别模型失败的原因和位置，可能会发现错误的标签并在必要时修正它们。一种方法是使用主动学习。

### 4\. 更重视质量而非数量

如果你被教导更多的数据就更好，你绝对不是唯一一个这样认为的人：这是机器学习中最常见的误解之一。然而，重要的不是数据的量，而是数据的多样性。规模只是被过分夸大了。显然，你需要一些数据来启动，但大量的数据不可避免地会导致收益递减——这纯粹是经济学问题。

相反，通常将时间和金钱投入到获取战略性选择的训练数据集的正确标签中，比投入大量无用数据的标注更为有益。确保数据策划（即抽样最有影响力的训练记录）融入机器学习生命周期应成为未来几年 MLOps 的关键关注点。

如果你像大多数数据科学家一样对数据标注感到沮丧，可能是时候尝试所有这些想法了。就像在敏捷的早期阶段一样，虽然这些原则本身并不特别困难，但它们都需要自律和意识。

使这些最佳实践融入全球数据科学家的日常习惯还需要很长的路要走，但像任何有意义的改变一样，它始于一个。记住，早在 2001 年，在滑雪胜地的一次会议就足以启动了导致软件开发革命的引擎。我们的革命可能已经在我们意想不到的眼前展开——实际上，它很可能已经展开了。所以请保持关注，享受这段旅程。

**简介： [詹妮弗·普伦德基博士](https://www.linkedin.com/in/jennifer-prendki/)** 是 Alectio 的创始人兼首席执行官，这是一家首个基于机器学习的数据准备运维平台。她和她的团队致力于帮助机器学习团队用更少的数据构建模型，并消除与“传统”数据准备相关的所有痛点。在创办 Alectio 之前，詹妮弗曾担任 Figure Eight 的机器学习副总裁；她还在 Atlassian 从零开始建立了一个完整的机器学习职能，并在 Walmart Labs 的搜索团队领导了多个数据科学项目。她被公认为是主动学习和机器学习生命周期管理领域的顶尖行业专家，并且是一位出色的演讲者，喜欢面对技术和非技术观众。

**相关内容：**

+   [噪声标签如何影响机器学习模型](https://www.kdnuggets.com/2021/04/imerit-noisy-labels-impact-machine-learning.html)

+   [数据标注如何促进 AI 模型](https://www.kdnuggets.com/2019/10/data-labeling-facilitates-ai-models.html)

+   [数据科学可以敏捷吗？将最佳敏捷实践应用到您的数据科学流程中](https://www.kdnuggets.com/2021/01/data-science-agile-best-practices.html)

* * *

## 我们的前三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速开启网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织进行 IT 工作

* * *

### 了解更多相关话题

+   [机器学习的数据标注：市场概况、方法和工具](https://www.kdnuggets.com/2021/12/data-labeling-ml-overview-and-tools.html)

+   [我如何使用 Grounding DINO 进行自动图像标注](https://www.kdnuggets.com/2023/05/automatic-image-labeling-grounding-dino.html)

+   [掌握数据科学项目管理的 7 个步骤与敏捷方法](https://www.kdnuggets.com/2023/07/7-steps-mastering-data-science-project-management-agile.html)

+   [关于数据管理你需要知道的 6 件事及其重要性…](https://www.kdnuggets.com/2022/05/6-things-need-know-data-management-matters-computer-vision.html)

+   [你需要合成数据的 5 个理由](https://www.kdnuggets.com/2023/02/5-reasons-need-synthetic-data.html)

+   [为什么你需要在 2022 年学习 Python](https://www.kdnuggets.com/2022/04/need-learn-python-2022.html)
