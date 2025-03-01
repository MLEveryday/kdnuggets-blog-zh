# 利用 BigQuery ML 为数据分析师简化机器学习

> 原文：[`www.kdnuggets.com/machine-learning-made-simple-for-data-analysts-with-bigquery-ml`](https://www.kdnuggets.com/machine-learning-made-simple-for-data-analysts-with-bigquery-ml)

![利用 BigQuery ML 为数据分析师简化机器学习](img/8badc466f2a74333c9f3a3900f93d8e7.png)

图片由 [freepik](https://www.freepik.com/free-vector/hand-drawn-flat-design-npl-illustration_22379566.htm#fromView=search&page=1&position=21&uuid=c879c91c-0a8c-48ea-b9e8-91f99bccee38) 提供

数据分析正经历一场革命。[机器学习 (ML)](https://cloud.google.com/bigquery/docs/bqml-introduction)，曾经是数据科学家的专属领域，现在对像你这样的数据分析师也变得触手可及。借助像 BigQuery ML 这样的工具，你可以利用机器学习的强大功能，而不需要计算机科学学位。让我们来探讨一下如何开始。

* * *

## 我们的前三个课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业道路。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析水平

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你所在组织的 IT 工作

* * *

## 什么是 BigQuery？

[BigQuery](https://cloud.google.com/bigquery/docs/introduction) 是一个完全托管的企业数据仓库，帮助你管理和分析数据，内置机器学习、地理空间分析和商业智能等功能。BigQuery 的无服务器架构允许你使用 SQL 查询来回答组织中最重要的问题，无需管理基础设施。

## 什么是 BigQuery ML？

[BigQuery ML (BQML)](https://cloud.google.com/bigquery/docs/bqml-introduction) 是 BigQuery 中的一项功能，允许你使用标准 SQL 查询来构建和执行机器学习模型。这意味着你可以利用现有的 SQL 技能来执行以下任务：

+   **预测分析：** 预测销售、客户流失或其他趋势。

+   **分类：** 对客户、产品或内容进行分类。

+   **推荐引擎：** 基于用户行为推荐产品或服务。

+   **异常检测：** 识别数据中的异常模式。

## 为什么选择 BigQuery ML？

接受 BigQuery ML 有几个令人信服的理由：

+   **无需 Python 或 R 编码：** 告别 Python 或 R。BigQuery ML 允许你使用熟悉的 SQL 语法来创建模型。

+   **可扩展：** BigQuery 的基础设施设计用于处理海量数据集。你可以在数 TB 的数据上训练模型，而不必担心资源限制。

+   **集成：** 你的模型与数据所在的位置相同。这简化了模型管理和部署，使得将预测直接纳入现有报告和仪表板变得轻而易举。

+   **速度：** BigQuery ML 利用 Google 强大的计算基础设施，实现更快的模型训练和执行。

+   **成本效益：** 仅为训练和预测过程中使用的资源付费。

## 谁能从 BigQuery ML 中受益？

如果你是一个希望在分析中增加预测能力的数据分析师，BigQuery ML 是一个很好的选择。无论你是在预测销售趋势、识别客户细分，还是检测异常，BigQuery ML 都可以帮助你获得有价值的洞察，而无需深入的机器学习专业知识。

## 你的第一步

**1\. 数据准备：** 确保你的数据是干净的、有组织的，并且在 BigQuery 表中。这对任何机器学习项目都至关重要。

**2\. 选择模型：** BQML 提供各种模型类型：

+   **线性回归：** 预测数值（例如销售预测）。

+   **逻辑回归：** 预测类别（例如客户流失——是或否）。

+   **聚类：** 将相似的项目归为一类（例如客户细分）。

+   **更多功能：** 时间序列模型、推荐系统的矩阵分解，甚至是用于高级情况的 TensorFlow 集成。

**3\. 构建和训练：** 使用简单的 SQL 语句创建和训练你的模型。 BQML 处理背后的复杂算法。

这是一个基于面积预测房价的基本示例：

```py
CREATE OR REPLACE MODEL `mydataset.housing_price_model`
OPTIONS(model_type='linear_reg') AS
SELECT price, square_footage FROM `mydataset.housing_data`;
SELECT * FROM ML.TRAIN('mydataset.housing_price_model');
```

**4\. 评估：** 检查你的模型表现如何。 BQML 提供如准确率、精确率、召回率等指标，具体取决于你的模型类型。

```py
SELECT * FROM ML.EVALUATE('mydataset.housing_price_model');
```

**5\. 预测：** 进入有趣的部分！使用你的模型对新数据进行预测。

```py
SELECT * FROM ML.PREDICT('mydataset.housing_price_model', 
    (SELECT 1500 AS square_footage));
```

## 高级功能和注意事项

+   [**超参数调整**](https://cloud.google.com/bigquery/docs/hp-tuning-overview)**：** BigQuery ML 允许你调整超参数来微调模型的性能。

+   [**可解释的 AI**](https://cloud.google.com/bigquery/docs/xai-overview#:~:text=Explainable%20AI%20helps%20you%20understand,contributed%20to%20the%20predicted%20result.)**：** 使用类似于可解释的 AI 的工具来理解影响模型预测的因素。

+   [**监控**](https://cloud.google.com/bigquery/docs/model-monitoring-overview)**：** 持续监控你的模型表现，并在新数据可用时根据需要重新训练模型。

## 成功的小贴士

+   **从简单开始：** 从一个简单的模型和数据集入手，以了解整个过程。

+   **实验：** 尝试不同的模型类型和设置，以找到最适合的。

+   **学习：** Google Cloud 提供了关于 BigQuery ML 的优秀文档和教程。

+   **社区：** 加入论坛和在线小组，与其他 BQML 用户交流。

## BigQuery ML：你的机器学习入门门户

BigQuery ML 是一个强大的工具，为数据分析师普及了机器学习。凭借其易用性、可扩展性和与现有工作流的集成，利用机器学习的力量来从数据中获取更深入的见解从未如此简单。

BigQuery ML 使你能够使用标准 SQL 查询来开发和[执行机器学习模型](https://cloud.google.com/bigquery/docs/e2e-journey)。此外，它还允许你利用[Vertex AI](https://cloud.google.com/bigquery/docs/generative-ai-overview) 模型和[Cloud AI API](https://cloud.google.com/bigquery/docs/ai-application-overview) 进行各种 AI 任务，例如生成文本或翻译语言。此外，Google Cloud 的 Gemini 通过 AI 驱动的功能增强了 BigQuery，简化了你的任务。有关 BigQuery 中这些 AI 能力的全面概述，请参阅[BigQuery 中的 Gemini](https://cloud.google.com/gemini/docs/bigquery/overview)。

开始尝试，今天就为你的分析解锁新的可能性！

**[Nivedita Kumari](https://www.linkedin.com/in/nivedita-kumari/)** 是一位经验丰富的数据分析和人工智能专业人士，拥有超过 8 年的经验。在她目前的角色中，作为 Google 的数据分析客户工程师，她与高管不断互动，帮助他们设计数据解决方案，并指导他们在 Google Cloud 上构建数据和机器学习解决方案的最佳实践。Nivedita 在伊利诺伊大学厄本那-香槟分校获得了数据分析方向的技术管理硕士学位。她希望普及机器学习和人工智能，打破技术障碍，让每个人都能参与这项变革性技术。她通过创建教程、指南、观点文章和编码演示，与开发者社区分享她的知识和经验。[在 LinkedIn 上与 Nivedita 连接](https://www.linkedin.com/in/nivedita-kumari/)。

### 更多相关主题

+   [Pydantic 教程：Python 中的数据验证变得简单](https://www.kdnuggets.com/pydantic-tutorial-data-validation-in-python-made-simple)

+   [组合 Pandas 数据框变得简单](https://www.kdnuggets.com/2022/09/combining-pandas-dataframes-made-simple.html)

+   [个性化 AI 变得简单：你的无代码 GPT 适配指南](https://www.kdnuggets.com/personalized-ai-made-simple-your-no-code-guide-to-adapting-gpts)

+   [Ollama 教程：本地运行 LLM 变得超级简单](https://www.kdnuggets.com/ollama-tutorial-running-llms-locally-made-super-simple)

+   [数据分析师和数据科学家之间的区别是什么？](https://www.kdnuggets.com/2022/03/difference-data-analysts-data-scientists.html)

+   [数据分析师的 SQL 和 Python 面试问题](https://www.kdnuggets.com/2023/02/sql-python-interview-questions-data-analysts.html)
