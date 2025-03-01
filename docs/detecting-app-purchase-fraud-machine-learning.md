# 使用机器学习检测应用内购买欺诈

> 原文：[`www.kdnuggets.com/2015/11/detecting-app-purchase-fraud-machine-learning.html`](https://www.kdnuggets.com/2015/11/detecting-app-purchase-fraud-machine-learning.html)

![c](img/3d9c022da2d331bb56691a9617b91b90.png) 评论

**作者：Ella Gati，[Soomla](http://soom.la/)**。

![检测欺诈](img/ab29ff4938f17b9d142fb4fed194168d.png)黑客应用程序如 [Freedom](http://onhax.net/freedom-iap-apk)、[iAP Cracker](http://www.cydiainsider.com/iap-cracker)、[iAPFree](http://www.cydiainsider.com/iapfree) 等允许用户免费进行应用内购买。通过这些黑客手段，玩家可以在没有支付任何费用的情况下获得他们购买的金币、宝石、关卡或生命。如果游戏开发者没有在应用内购买上实施任何验证过程，例如 [SOOMLA 的欺诈保护](http://know.soom.la/unity/grow/grow_fraudprotection)，这些购买将被记录为系统中的真实购买。因此，报告的收入可能与实际收入大相径庭（尤其是在存在大量欺诈的热门游戏中）。

我们希望使报告尽可能准确，并能够向游戏开发者传达他们游戏的真实状态。我们使用机器学习和统计建模技术来解决这个问题。

在 GROW 数据网络中借助几款大型游戏的帮助，我们成功构建了一个模型，能够以非常高的准确率将每次购买分类为真实或欺诈。

### 应用内购买模型特征

该模型使用了各种购买、用户和物品特征。下表详细列出了我们计算的一部分特征：

| **购买** | **用户** | **物品** |
| --- | --- | --- |
| 购买日期 | 总购买次数 | 总购买次数 |
| 购买时间 | 总收入 | 总收入 |
| 购买来源的国家 | 平均每日收入 | 平均每日购买次数 |
| 购买所用的货币 | 用户玩过的游戏数量 | 平均每日收入 |
| 手机地区设置是否与国家匹配 | 用户购买的游戏数量 | 最大每日购买次数 |
| 购买货币是否与国家的货币匹配 | 用户是否曾被收据验证阻止 | 最大每日收入 |
| … | … | … |

### 决策树的救援

决策树，顾名思义，是帮助决策的树。树的每个内部节点测试一个特征的值，叶节点则是目标类别。给定一个新的观察值，可以用树来决定将其分配到哪个类别。

在我们的案例中，树可以有两种叶子节点（类别）：欺诈或非欺诈，特征是上述详细说明的内容。内部节点的例子可以是“总购买次数 > 100”或“货币与国家匹配 = 真”。为了避免过拟合训练数据，基于树的技术结合了多个树，以获得比每个单独树输出更准确的最终结果。

基于树的分类算法有许多优点，列举几项：

+   参数之间的非线性关系不会影响树的性能。

+   决策树隐式地执行变量筛选或特征选择。

+   决策树需要相对较少的数据准备，并且易于解释和理解。

我们尝试了两种基于树的分类器。随机森林分类器是一个决策树的集合，训练在数据的子集上，它输出的是单个树输出的类别的众数。提升树使用梯度提升技术结合多个决策树，拟合简单树的加权加性扩展。

另一个模型参数是类别权重，它有两种形式：均匀的，即所有类别的权重都是 1，以及按类别的，即使用类别在整体人口中的相对大小作为类别权重。

### 欺诈分类性能

我们通过四个指标来衡量模型的性能：

+   准确率：所有测试数据中正确分类的比例。

+   假阳性率 (FPR)：所有有效购买中被错误分类为欺诈的比例。

+   假阴性率 (FNR)：所有欺诈购买中被错误分类为非欺诈的比例。

+   F1 分数：**[精确度和召回率](https://en.wikipedia.org/wiki/Precision_and_recall)** 的调和平均值，这是一个来自信息检索领域的度量，反映了其他两个指标之间的平衡。

将有效购买和用户分类为欺诈的错误比错过一个欺诈购买要严重得多，因此我们旨在将假阳性率降低到最低，即使这会导致假阴性率略高。

我们的真实数据包括来自 4 个游戏的购买数据。在其中最大的一个游戏中，我们有 145K 购买的标签。对于这两种算法，参数是通过交叉验证进行调整的。

### 每游戏模型

对于第一次实验，我们为每个游戏构建了不同的模型。下表详细说明了不同游戏和模型参数的性能。

| **游戏** | **分类器** | **类别权重** | **FPR** | **FNR** | **F1 分数** | **准确率** |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | 随机森林 | 均匀 | 0.22 | 0.03 | 0.95 | 0.93 |
| 1 | 随机森林 | 按类别 | 0.10 | 0.08 | 0.95 | 0.92 |
| 1 | 提升树 | 均匀 | 0.09 | 0.03 | **0.97** | 0.96 |
| 1 | 提升树 | 按类别 | **0.05** | 0.05 | 0.96 | 0.95 |
| 2 | 随机森林 | 均匀 | 0.02 | 0.16 | 0.89 | 0.85 |
| 2 | 随机森林 | 按类别 | 0.01 | 0.16 | 0.91 | 0.82 |
| 2 | 提升树 | 均匀 | **0.01** | 0.11 | **0.94** | 0.84 |
| 2 | 增强树 | 按类别 | 0.05 | 0.05 | 0.90 | 0.85 |

这些结果非常令人印象深刻！每个游戏模型的 F1 分数高达 97%。

第二个游戏的真实数据较少（这是一个每月平均购买次数少 100 倍的游戏，我们获得了一个月的购买数据），这解释了其较低的性能。

增强树算法优于随机森林算法，这并不令人惊讶，因为它是一种优化，通常可以在较少的树木中提供更好的准确性。

使用按类别大小调整的权重通常会导致更低的假阳性率（FPR）和更高的假阴性率（FNR），F1 分数略低。如前所述，我们更关心假阳性率，因此在后续实验中我们使用了具有非均匀权重的增强树算法。

### 跨游戏分类

我们已经看到，当为特定游戏构建模型时，可以获得非常好的结果。但我们只有四个游戏的真实数据。那么其他游戏怎么办？

为了测试这一点，第二个实验在一个包含来自一个游戏的数据的训练集和来自另一个游戏的数据的测试集上进行。

![准确性热力图](img/14ce57eb9cb840125ddfdfea237073bb.png)

上表展示了跨游戏实验的准确性。所有分数都为 79%或更高！这对其他所有游戏来说都是好消息。正如预期的，当训练集和测试集来自相同的游戏数据（70%-30%的随机拆分）时，获得了最高的分数。最低的分数是在测试第 4 个游戏时获得的，它是最小的游戏（200 次购买）。

另一个有趣的结果是本实验中的 FPR 分数。

![FPR 热力图](http://blog.soom.la/wp-content/uploads/2015/11/FPRHeatMap1.png)

同时值得注意的是，训练于游戏 4 的模型生成了较差的假阳性率（FPR）分数。这是由于购买数量少，以及欺诈行为相对较低（54%对比于其他游戏的 77%-85%）。由于游戏 1 具有最大的真实数据，训练于其他（较小的）游戏的模型假阳性率非常高，最多有 30%的有效购买被分类为欺诈。当训练于其他游戏时，我们得到的结果要好得多，错误分类的有效购买率为 1-2%。

这一实验证明了游戏之间的数据传输在大多数情况下效果良好，但如果你的游戏具有非常独特的用户行为，可能会出现问题。

### 结果

最终，我们在所有的真实数据上训练了一个模型，并用它对我们数据库中的所有购买进行分类。根据分类器的结果，55.7%的购买是欺诈行为，这些购买占总收入的 72.9%。

![按游戏大小的欺诈百分比 - SOOMLA](http://blog.soom.la/wp-content/uploads/2015/11/fraud-percentage-by-game-size.png)

这些数字在不同游戏之间有所不同。我们可以看到一个普遍趋势：较大的游戏（用户更多的游戏）的欺诈百分比最高，即使我们也看到一些相对较小的游戏有高达 89%的欺诈。这些差异可以通过不同的经济模型或游戏在不同国家的受欢迎程度来解释。

根据我们的模型结果，欺诈在斯拉夫国家最为普遍。俄罗斯、乌克兰和白俄罗斯排名前列，超过 90%的购买都是欺诈行为。

![每个国家的欺诈率 - SOOMLA](http://blog.soom.la/wp-content/uploads/2015/11/fraud-rate-per-country.png)

模型预测仅有 2%的用户有一些有效购买和一些欺诈。其余 98%的用户要么是欺诈者（总是进行欺诈），要么不是（所有购买都有效）。在这 98%中，超过一半是欺诈者。

### 对游戏开发者的影响

知道哪些用户是欺诈者可以帮助游戏开发者调整游戏玩法并采取限制措施以确保最小的收入损失。一些选项包括：

+   完全阻止特定用户的应用内购买。

+   增加游戏难度以阻止用户使用黑客获取的游戏币进行非正常进度。

+   增加广告频率以最大化从永远不会付费的滥用用户那里获得的收入。

+   使游戏无法进行，例如，通过突出警告信息来禁用所有游戏玩法，要求用户立即进行应用内购买存款以解锁游戏。

### 我们如何改进？

我们掌握的真实数据越多，我们的分类结果就会越好。游戏开发者和工作室可以通过提供反馈或与我们分享销售报告来获得更好的报告并帮助我们改进。

有问题？请联系 ella@soom.la。

[本文首次出现在 Soomla 博客上](http://blog.soom.la/2015/11/detecting-app-purchase-fraud-machine-learning.html)。

**相关：**

+   数据挖掘医疗数据 – 我们能发现什么？

+   如何使用 Hadoop 和大数据发现被盗数据？

+   欺诈检测解决方案

* * *

## 我们的前三个课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [Google 网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 加速你的网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [Google 数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [Google IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持组织的 IT

* * *

### 更多相关话题

+   [使用 Eurybia 检测数据漂移以确保生产 ML 模型质量](https://www.kdnuggets.com/2022/07/detecting-data-drift-ensuring-production-ml-model-quality-eurybia.html)

+   [5 款免费工具用于检测 ChatGPT、GPT3 和 GPT2](https://www.kdnuggets.com/2023/02/5-free-tools-detecting-chatgpt-gpt3-gpt2.html)

+   [检测 ChatGPT、GPT-4、Bard 和 Claude 的十大工具](https://www.kdnuggets.com/2023/05/top-10-tools-detecting-chatgpt-gpt4-bard-llms.html)

+   [在 5 分钟内构建机器学习 Web 应用](https://www.kdnuggets.com/2022/03/build-machine-learning-web-app-5-minutes.html)

+   [KDnuggets 新闻 2022 年 3 月 9 日：在 5 分钟内构建机器学习 Web 应用…](https://www.kdnuggets.com/2022/n10.html)

+   [使用 Heroku 部署机器学习 Web 应用](https://www.kdnuggets.com/2022/04/deploy-machine-learning-web-app-heroku.html)
