# 使用 Azure 机器学习服务构建推荐系统

> 原文：[`www.kdnuggets.com/2019/05/recommender-systems-azure-machine-learning.html`](https://www.kdnuggets.com/2019/05/recommender-systems-azure-machine-learning.html)

![c](img/3d9c022da2d331bb56691a9617b91b90.png) 评论

**由 [Heather Spetalnick](https://www.linkedin.com/in/heather-spetalnick-16674445/)，程序经理，ML 平台**

![](img/ed696d137e2bad6fe0d95f208557ef45.png)

推荐系统在零售、新闻和媒体等多个行业中都有应用。如果你曾经使用过流媒体服务或电子商务网站，并根据你之前观看或购买的内容收到过推荐，那么你就与推荐系统互动过。随着大量数据的可用性，许多企业将推荐系统作为关键的收入驱动因素。然而，找到合适的推荐算法对于数据科学家来说可能非常耗时。这就是微软提供一个[GitHub 存储库](https://github.com/Microsoft/Recommenders/tree/master/)的原因，该存储库包含了 Python 最佳实践示例，以方便使用[Azure 机器学习服务](https://azure.microsoft.com/en-us/services/machine-learning-service/)来构建和评估推荐系统。

### 什么是推荐系统？

推荐系统主要有两种类型：协同过滤和基于内容的过滤。协同过滤（常用于电子商务场景）识别用户与他们评价的项目之间的互动，以推荐他们未见过的新项目。基于内容的过滤（常用于流媒体服务）识别关于用户档案或项目描述的特征，以推荐新内容。这些方法也可以结合起来用于混合方法。

推荐系统使客户在企业网站上停留更长时间，他们与更多的产品/内容互动，并且建议客户可能会购买或参与的产品或内容，就像商店销售助理可能会做的那样。下面，我们将向你展示这个存储库是什么，它是如何缓解数据科学家在构建和实施推荐系统时的痛点的。

### 缓解数据科学家的工作过程

推荐算法 GitHub 存储库提供了用于构建推荐系统的示例和最佳实践，这些示例以 Jupyter notebooks 的形式提供。示例详细说明了我们在五个关键任务上的经验：

+   [数据准备](https://github.com/Microsoft/Recommenders/blob/master/notebooks/01_prepare_data/README.md) - 为每个推荐算法准备和加载数据

+   [建模](https://github.com/Microsoft/Recommenders/blob/master/notebooks/02_model/README.md)- 使用各种经典和深度学习推荐算法如交替最小二乘法 ([ALS](https://spark.apache.org/docs/latest/api/python/_modules/pyspark/ml/recommendation.html#ALS)) 或极端深度因子分解机 (xDeepFM) 构建模型

+   [评估](https://github.com/Microsoft/Recommenders/blob/master/notebooks/03_evaluate/README.md)- 使用离线指标评估算法

+   [模型选择和优化](https://github.com/Microsoft/Recommenders/blob/master/notebooks/04_model_select_and_optimize)- 调整和优化推荐模型的超参数

+   [操作化](https://github.com/Microsoft/Recommenders/blob/master/notebooks/05_operationalize/README.md)- 在 Azure 上操作化生产环境中的模型

[reco utils](https://github.com/Microsoft/Recommenders/blob/master/reco_utils) 提供了几种工具，以支持加载不同算法预期格式的数据集、评估模型输出以及拆分训练/测试数据等常见任务。提供了几种最先进算法的实现，以便在组织或数据科学家的应用中进行自学和定制。

在下图中，你将找到仓库中可用的推荐算法列表。我们一直在增加更多推荐算法，所以请访问 GitHub 仓库以查看最新列表。

![](img/f1241b944942209f2376f822dd801d2e.png)

### 让我们更详细地了解推荐系统仓库如何解决数据科学家的痛点。

### 1. 评估不同推荐算法选项耗时

+   推荐系统 GitHub 仓库的一个主要优点是它提供了一组选项，并展示了哪些算法最适合解决特定类型的问题。它还提供了一个粗略的框架来切换不同的算法。如果模型性能准确度不够，需要更适合实时结果的算法，或者最初选择的算法不适合使用的数据类型，数据科学家可能需要切换到不同的算法。

### 2. 选择、理解和实现新的推荐系统模型可能成本高昂

+   从头开始选择合适的推荐算法并实现新的推荐系统模型可能成本高昂，因为这些模型需要大量的训练和测试时间以及计算能力。推荐的 GitHub 仓库简化了选择过程，通过节省数据科学家在测试许多不适合其项目/场景的算法上的时间，从而降低了成本。此外，结合[Azure 的各种定价选项](https://azure.microsoft.com/en-us/pricing/)，减少了数据科学家在测试上的费用以及组织在部署上的成本。

### 实施更多最先进的算法可能看起来令人望而生畏

+   当被要求构建推荐系统时，数据科学家通常会转向更常见的算法，以减轻选择和测试更先进算法所需的时间和成本，即使这些更先进的算法可能更适合项目/数据集。推荐系统的 GitHub 代码库提供了一些知名和最先进的推荐算法，适合特定场景。它还提供了最佳实践，遵循这些实践会使实现更先进的算法变得更容易。

### 数据科学家对如何使用 Azure 机器学习服务来训练、测试、优化和部署推荐算法不熟悉

+   最后，推荐系统的 GitHub 代码库提供了如何在 Azure 和[Azure 机器学习 (Azure ML) 服务](https://docs.microsoft.com/azure/machine-learning/service/)上训练、测试、优化和部署推荐模型的最佳实践。实际上，有[几个可用的笔记本](https://github.com/Microsoft/Recommenders/tree/master/notebooks#submit-an-existing-notebook-to-azure-machine-learning)演示了如何在 Azure ML 服务上运行代码库中的推荐算法。数据科学家还可以将任何已创建的笔记本提交到 Azure，几乎无需修改。

### Azure ML 可以在各种笔记本中广泛用于 AI 模型开发相关任务，例如：

+   超参数调优

+   跟踪和监控指标以提升模型创建过程

+   在 DSVM 和 Azure ML 计算中进行规模扩展

+   将 Web 服务部署到 Azure Kubernetes 服务

+   提交管道

### 了解更多

利用[GitHub 代码库创建你自己的推荐系统](https://github.com/Microsoft/Recommenders/tree/master/)。

了解更多关于[Azure 机器学习服务](https://azure.microsoft.com/en-us/services/machine-learning-service/)的信息。

开始试用[Azure 机器学习服务](https://azure.microsoft.com/en-us/trial/get-started-machine-learning/)。

[原文](https://azure.microsoft.com/en-us/blog/building-recommender-systems-with-azure-machine-learning-service/)。经许可转载。

**简介**：[Heather Spetalnick](https://www.linkedin.com/in/heather-spetalnick-16674445/)是微软在马萨诸塞州剑桥的项目经理，负责 Azure 机器学习的用户体验工作。

**资源：**

+   [在线和基于 Web 的：分析、数据挖掘、数据科学、机器学习教育](https://www.kdnuggets.com/education/online.html)

+   [用于分析、数据科学、数据挖掘和机器学习的软件](https://www.kdnuggets.com/software/index.html)

**相关：**

+   [K-Means 聚类：推荐系统的无监督学习](https://www.kdnuggets.com/2019/04/k-means-clustering-unsupervised-learning-recommender-systems.html)

+   [构建推荐系统](https://www.kdnuggets.com/2019/04/building-recommender-system.html)

+   [为意外情况做好准备](https://www.kdnuggets.com/2019/02/preparing-unexpected.html)

* * *

## 我们的三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升您的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持您的组织进行 IT

* * *

### 更多相关内容

+   [使用 Python 为亚马逊产品构建推荐系统](https://www.kdnuggets.com/2023/02/building-recommender-system-amazon-products-python.html)

+   [311 呼叫中心表现：服务水平评级](https://www.kdnuggets.com/2023/03/boxplot-outlier-311-call-center-performance.html)

+   [通过 DataCamp 的新 Azure 认证提升水平](https://www.kdnuggets.com/level-up-with-datacamps-new-azure-certification)

+   [设计有效且可靠的机器学习系统！](https://www.kdnuggets.com/2023/05/manning-design-effective-reliable-machine-learning-systems.html)

+   [人工智能系统中的不确定性量化](https://www.kdnuggets.com/2022/04/uncertainty-quantification-artificial-intelligencebased-systems.html)

+   [实施推荐系统的十个关键经验](https://www.kdnuggets.com/2022/07/ten-key-lessons-implementing-recommendation-systems-business.html)
