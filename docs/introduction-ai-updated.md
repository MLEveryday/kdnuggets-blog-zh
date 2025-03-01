# AI 简介，更新版

> 原文：[`www.kdnuggets.com/2020/10/introduction-ai-updated.html`](https://www.kdnuggets.com/2020/10/introduction-ai-updated.html)

评论

**由 [Imtiaz Adam](https://www.linkedin.com/in/imtiaz-adam-7467528/)，AI 和战略执行官**。

![](img/5614254a8b13081cd0ee0f9b27469457.png)

* * *

## 我们的三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业的轨道。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你组织的 IT 工作

* * *

### 什么是人工智能（AI）

AI 涉及开发能够执行人类擅长的任务的计算系统，例如识别物体、理解和分析语言，以及在受限环境中做出决策。

**窄域 AI：** AI 的一个领域，机器被设计用来执行单一任务，并且机器在执行该任务时非常出色。然而，一旦机器训练完成，它不会推广到未见领域。这是我们今天拥有的 AI 形式，例如 Google 翻译。

**人工通用智能（AGI）：** 一种可以完成任何人类能够做的智力任务的 AI 形式。它更具意识，并做出类似于人类决策的决定。AGI 目前仍然是一个理想，关于它的到来，各种预测从 2029 年到 2049 年甚至可能永远无法实现。它可能在未来 20 年左右到来，但面临与硬件、今日强大机器的能耗需求以及解决影响即使是最先进深度学习算法的灾难性记忆丧失等挑战。

**超级智能：** 是一种在所有领域的表现超越人类的智能（根据 Nick Bostrom 的定义）。这涉及到一般智慧、问题解决和创造力等方面。

![](img/71f0752840fd69b264a2f63a0b75dd0a.png)

**经典人工智能：**包括基于规则的系统、搜索算法（如无信息搜索（广度优先、深度优先、普遍成本搜索）和有信息搜索如 A 和 A*算法）。这些奠定了今天更先进的方法的坚实基础，这些方法更适合大规模搜索空间和大数据集。它还包括逻辑方法，如命题和谓词演算。虽然这些方法适用于确定性场景，但现实世界中的问题往往更适合概率方法。

该领域近年来在各个行业中产生了重大影响，包括医疗保健、金融服务、零售、营销、交通、安全、制造和旅行行业。

大数据的出现，由互联网、智能移动设备和社交媒体的到来推动，使得 AI 算法，特别是机器学习和深度学习，能够利用大数据并更优化地执行任务。加上更便宜、更强大的硬件，如图形处理单元（GPU），使 AI 发展成更复杂的架构。

### 机器学习

机器学习被定义为应用统计方法使计算机系统从数据中学习以实现最终目标的 AI 领域。这个术语由 Arthur Samuel 在 1959 年引入。

**需要理解的关键术语**

特征/属性：用于将数据表示为算法可以理解和处理的形式。例如，图像中的特征可能表示边缘和角落。

熵：随机变量中的不确定性量。

信息增益：由一些先前知识带来的信息量。

监督学习：一种处理已标记（注释）数据的学习算法。例如，通过带有标记的水果图像学习将水果分类为苹果、橙子、柠檬等。

无监督学习：一种发现数据中隐藏模式的学习算法，数据未被标记（注释）。一个例子是将客户分成不同的群体。

半监督学习：当只有一小部分数据被标记时的学习算法。

[主动学习](https://en.wikipedia.org/wiki/Active_learning_(machine_learning))涉及一种算法可以主动询问教师标签的情况。[Jennifer Prendki](https://www.kdnuggets.com/2018/10/introduction-active-learning.html)定义为“……一种半监督学习（其中使用了标记和未标记的数据）……主动学习是指在训练阶段逐步和动态地标记数据，以使算法识别最有信息量的标签，从而更快地学习。”

损失函数：是实际情况与算法学习到的内容之间的差异。在机器学习中，目标是最小化损失函数，以便算法能够继续在未见过的场景中进行泛化和表现。

### 机器学习方法（非详尽列表）

分类、回归和聚类是机器学习的三个主要领域。

[分类](https://machinelearningmastery.com/classification-versus-regression-in-machine-learning/)被 Jason Brownlee 总结为“关于预测标签，而回归则是关于预测量。分类是预测离散类标签的任务。分类预测可以使用准确率进行评估，而回归预测则不能。”

[回归](https://machinelearningmastery.com/classification-versus-regression-in-machine-learning/)预测建模被 Jason Brownlee 总结为“任务是从输入变量（X）到连续输出变量（y）近似一个映射函数（f）。回归是预测一个连续量的任务。回归预测可以使用均方根误差进行评估，而分类预测则不能。”

[聚类](https://www.geeksforgeeks.org/clustering-in-machine-learning/)被 Surya Priy 总结为“将总体或数据点划分为若干组的任务，使得同一组中的数据点彼此之间更为相似，而与其他组中的数据点则不相似。它基本上是根据相似性和差异性对对象进行的集合。”

**强化学习：** 是一个处理在环境中建模代理的领域，该环境不断奖励代理做出正确决策。举例来说，代理在与人类对弈的国际象棋中获胜。当代理走出正确的棋步时会获得奖励，走错则会受到惩罚。经过训练后，该代理可以在真实比赛中与人类竞争。

**线性回归：** 是机器学习的一个领域，它建模两个或多个具有连续值的变量之间的关系。

**逻辑回归：** 是一种分类技术，它将 logit 函数建模为特征的线性组合。二元逻辑回归处理变量只有两个结果（‘0’或‘1’）的情况。多项逻辑回归处理预测变量可能有多个不同值的情况。

**k-均值：** 是一种无监督的方法，用于根据数据实例之间的相似性对其进行分组（或聚类）。一个例子是根据相似性对人口进行分组。

**K-最近邻（KNN）：** 是一种监督机器学习算法，可用于解决分类和回归问题。它基于这样一个假设：相似的项彼此靠近。

**支持向量机（SVM）：** 是一种分类算法，通过在两个数据类别之间绘制分隔超平面来进行分类。一旦训练完成，SVM 模型可以用作对未见数据的分类器。

**决策树：** 是一种从数据中学习决策规则的算法。这些规则随后用于决策制定。

**提升和集成：** 是将多个表现不佳的弱学习者组合成一个强分类器的方法。自适应提升（AdaBoost）可以应用于分类和回归问题，通过结合多个弱分类器来创建一个强分类器。最近的一些关键示例包括 [XG Boost](https://machinelearningmastery.com/gentle-introduction-xgboost-applied-machine-learning/)，它在 [Kaggle](https://www.kaggle.com/) 竞赛中对表格或结构化数据表现出色（参见 [Tianqi Chen 和 Carlos Guestrin](https://arxiv.org/pdf/1603.02754.pdf) 2016）， [微软在 2017 年推出的 Light Gradient Boosting Machine（Light GBM）](https://github.com/microsoft/LightGBM)，以及 [Yandex 在 2017 年推出的 CatBoost](https://yandex.com/dev/catboost/)。有关集成学习的更多信息，请参见 [Jason Brownlee 的集成学习文章](https://machinelearningmastery.com/gradient-boosting-with-scikit-learn-xgboost-lightgbm-and-catboost/) 和 [KDnuggets 发表的文章](https://www.kdnuggets.com/) 标题为 [CatBoost 与 Light GBM 与 XGBoost](https://www.kdnuggets.com/2018/03/catboost-vs-light-gbm-vs-xgboost.html)。

**随机森林：** 属于集成学习技术的范畴，通过在训练期间创建多个决策树来引入随机性。输出将是各个树的平均预测值或表示类别模式的类别。这可以防止算法过拟合或记忆训练数据。

**主成分分析（PCA）：** 是一种减少数据维度的方法，同时保持数据的可解释性。这有助于去除数据中冗余的信息，同时保留解释大部分数据的特征。

**同步定位与地图构建** (**SLAM**): 处理机器人在未知环境中定位自己的方法。

**进化遗传算法：** 这些算法受到生物学的启发，灵感来源于进化理论。它们通常用于解决优化和搜索问题，通过应用包括选择、交叉和变异在内的生物启发概念。

**神经网络：** 是受生物启发的网络，通过层级化方式从数据中提取抽象特征。神经网络在 1980 年代和 1990 年代曾遭到抑制。是**Geoff Hinton**继续推动了神经网络的发展，尽管当时许多经典人工智能社区对他嗤之以鼻。深度神经网络（参见下文定义）发展的关键时刻是在 2012 年，当时来自多伦多的一个团队在 ImageNet 竞赛中用 AlexNet 网络向世界展示了自己。他们的神经网络与之前使用手工提取特征的方法相比，大大减少了错误率。

### 深度学习

深度学习指的是具有多个隐藏层的神经网络领域。这样的神经网络通常被称为深度神经网络。

目前使用的几种主要深度神经网络类型包括：

**卷积神经网络（CNN）：** 卷积神经网络是一种通过卷积操作从输入数据中以层次化方式提取模式的神经网络。它主要用于具有空间关系的数据，例如图像。卷积操作通过在图像上滑动内核来提取与任务相关的特征。

**递归神经网络（RNN）：** 递归神经网络，特别是 LSTM，用于处理序列数据。例如，时间序列数据、股票市场数据、语音、传感器信号和能源数据具有时间依赖性。LSTM 是一种更高效的 RNN，缓解了梯度消失问题，使其能够记住短期和远期的信息。

**限制玻尔兹曼机（RBM）：** 基本上是一种具有随机属性的神经网络。限制玻尔兹曼机使用名为对比散度的方法进行训练。训练完成后，隐藏层是输入的潜在表示。RBM 学习输入的概率表示。

**深度置信网络：** 是由限制玻尔兹曼机组成的，每一层作为下一层的可见层。在向网络中添加额外层之前，每一层都经过训练，这有助于概率性地重建输入。该网络使用逐层无监督的方法进行训练。

**变分自编码器（VAE）：** 是一种改进版的自编码器，用于学习输入的最优潜在表示。它由一个编码器和一个解码器以及一个损失函数组成。VAE 使用概率方法，并涉及潜在高斯模型中的近似推断。

**生成对抗网络（GANs）**：生成对抗网络是一种使用生成器和判别器的卷积神经网络（CNN）。生成器不断生成数据，而判别器则学习区分虚假数据与真实数据。随着训练的进行，生成器不断提高生成看起来真实的虚假数据的能力，而判别器则更好地学习区分虚假和真实的数据，从而帮助生成器自我改进。训练完成后，我们可以使用生成器生成看起来很真实的虚假数据。例如，一个训练过脸部图像的 GAN 可以用来生成不存在的、非常真实的脸部图像。

**变换器**：用于处理序列数据，特别是在自然语言处理（NLP）领域中，处理文本数据的任务，如语言翻译。该模型于 2017 年在一篇名为"[Attention is All you Need](https://arxiv.org/abs/1706.03762)"的论文中首次提出。变换器模型的架构包括编码器和解码器的应用，以及自注意力机制，涉及到对输入序列中不同位置的关注能力，并生成序列的表示。与 RNN 相比，它们的优势在于不需要按序处理数据，这意味着在处理句子时，不需要先处理句子的开头再处理结尾。著名的变换器模型包括双向编码器表示（BERT）和 GPT 变体（来自 OpenAI）。

**深度强化学习**：深度强化学习算法涉及建模一个智能体，该智能体学习以尽可能最优的方式与环境互动。智能体不断采取行动，始终牢记目标，而环境则根据智能体的行动给予奖励或惩罚。通过这种方式，智能体学习以最优的方式行为，以实现目标。DeepMind 的 AlphaGo 是智能体学习下围棋并能够与人类竞争的最佳例子之一。

**胶囊网络**：仍然是一个活跃的研究领域。卷积神经网络（CNN）通常学习到的数据表示往往难以解释。另一方面，胶囊网络能够从输入中提取特定类型的表示，例如，它保留了物体部件之间的层次姿态关系。胶囊网络的另一个优势是它能够用比 CNN 所需的更少的数据学习表示。有关胶囊网络的更多信息，请参见[胶囊之间的动态路由](http://dynamic%20routing%20between%20capsules/)，[堆叠胶囊自编码器](https://arxiv.org/abs/1906.06818)和[DA-CapsNet：双重注意力机制胶囊网络](https://www.nature.com/articles/s41598-020-68453-w)。

**神经进化：**由[Kenneth O. Stanley](https://www.oreilly.com/radar/neuroevolution-a-different-kind-of-deep-learning/)定义为：“旨在触发一种与产生我们大脑的进化过程类似的进化过程，只不过是在计算机内部。换句话说，神经进化旨在通过进化算法来发展演化神经网络的方法。” [Uber Labs 的研究人员认为，神经进化](https://eng.uber.com/deep-neuroevolution/)方法在一定程度上由于降低了陷入局部最小值的可能性，与基于梯度下降的深度学习算法具有竞争力。[Stanley 等人](https://www.nature.com/articles/s42256-018-0006-z)表示：“我们的希望是激发对该领域的新兴趣，因为它满足了今天日益增加的计算能力的潜力，突显其许多想法如何为深度学习、深度强化学习和机器学习社区提供令人兴奋的灵感和混合资源，并解释神经进化如何在长期追求人工通用智能中证明是一个关键工具。”

**神经符号人工智能**：由[MIT-IBM Watson AILab](https://mitibmwatsonailab.mit.edu/category/neuro-symbolic-ai/)定义为一种将神经网络（从原始数据文件中提取统计结构——例如图像和声音文件的背景）与问题和逻辑的符号表示结合起来的 AI 方法的融合。“通过融合这两种方法，我们正在构建一种新型的 AI，其能力远超其部分之和。这些神经符号混合系统需要较少的训练数据，并跟踪进行推理和得出结论所需的步骤。它们在跨领域转移知识时也更为轻松。我们相信，这些系统将引领 AI 的新纪元，让机器更像人类一样学习，通过将词语与图像连接起来，掌握抽象概念。”

**联邦学习**：也称为**协作学习**，在[维基百科](https://en.wikipedia.org/wiki/Federated_learning)中定义为一种机器学习技术，使得算法可以在多个去中心化的服务器（或设备）上进行训练，而无需交换本地数据。[差分隐私](https://arxiv.org/abs/2007.00914)旨在通过衡量联邦学习元素间通信的隐私损失来增强数据隐私保护。这项技术可能解决数据隐私和安全的关键挑战，涉及异构数据，并影响物联网（IoT）、医疗保健、银行、保险等领域，在这些领域数据隐私和协作学习至关重要，并且随着 AI IoT 的扩展，可能会成为 5G 和边缘计算时代的关键技术。

[原文](https://www.linkedin.com/pulse/introduction-ai-imtiaz-adam/)。经许可转载。

**简介：** [Imtiaz Adam](https://www.linkedin.com/in/imtiaz-adam-7467528/)，计算机科学硕士（人工智能与机器学习工程师）和斯隆战略研究员，MBA，专注于人工智能和机器学习技术的开发，特别是深度学习方面。

**相关：**

+   [我们距离实现人工通用智能的 3 个原因](https://www.kdnuggets.com/2020/04/3-reasons-far-from-artificial-general-intelligence.html)

+   [2020 年值得阅读的人工智能论文](https://www.kdnuggets.com/2020/09/ai-papers-read-2020.html)

+   [13 篇人工智能专家必读的论文](https://www.kdnuggets.com/2020/05/13-must-read-papers-ai-experts.html)

### 更多相关主题

+   [停止学习数据科学以寻找目标，然后寻找目标来……](https://www.kdnuggets.com/2021/12/stop-learning-data-science-find-purpose.html)

+   [一个 90 亿美元的人工智能失败案例，审视](https://www.kdnuggets.com/2021/12/9b-ai-failure-examined.html)

+   [学习数据科学统计的顶级资源](https://www.kdnuggets.com/2021/12/springboard-top-resources-learn-data-science-statistics.html)

+   [成功数据科学家的 5 个特征](https://www.kdnuggets.com/2021/12/5-characteristics-successful-data-scientist.html)

+   [是什么让 Python 成为初创公司的理想编程语言](https://www.kdnuggets.com/2021/12/makes-python-ideal-programming-language-startups.html)

+   [每个数据科学家都应该知道的三个 R 语言库（即使你使用 Python）](https://www.kdnuggets.com/2021/12/three-r-libraries-every-data-scientist-know-even-python.html)
