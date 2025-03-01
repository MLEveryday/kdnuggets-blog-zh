# 匿名化与数据科学的未来

> 原文：[`www.kdnuggets.com/2017/04/anonymization-future-data-science.html`](https://www.kdnuggets.com/2017/04/anonymization-future-data-science.html)

![c](img/3d9c022da2d331bb56691a9617b91b90.png) 评论

**作者：Steve Touw，[Immuta](https://www.immuta.com/)的首席技术官兼联合创始人。**

管理数据隐私对于数据孤岛遍布的大型企业而言正变得越来越困难。新的数据法规——从[欧盟](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)到[美国](https://www.fcc.gov/document/fcc-adopts-broadband-consumer-privacy-rules)到[中国](https://www.dowjones.com/insights/examining-chinas-new-cybersecurity-law-china-recently-passed-new-cybersecurity-law-takes-effect-june-1-mean-companies-business/)——表明这一挑战才刚刚开始。

* * *

## 我们的前三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业道路。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 支持你的组织的 IT 工作

* * *

这一趋势突显了匿名化的重要性——这是数据科学家“隐私工具箱”中的重要工具之一。数据匿名化是一种技术，可以在保护数据中的私人信息的同时，保持数据的实用性，尽管这种保护程度有所不同；然而，正如我们将看到的，这种工具最好是与其他工具结合使用，而不是作为独立策略来保护你的数据。

这篇论文的基础是什么？简而言之，就是匿名化的实际限制。当然，还有贾德·阿帕图。

### 匿名化、实用性与贾德·阿帕图

首先，将匿名化视为一种从数据集中移除个人识别信息的技术，使剩余的数据无法与该个人关联。但这并不是终点：剩余的数据也需要实际上是有用的。这就是我所称的“隐私与实用性的权衡”。如果数据集被完全匿名化，那么从这些数据中识别出个人的风险就不存在，但这些数据也可能（并且很可能）变得无用。在网络安全领域，有一句话是最安全的计算机就是无法工作的计算机。在这里也是同样的道理：确保匿名性通常需要牺牲实用性。

在许多情况下，匿名化技术可能是“脆弱的”，也就是说，即使你认为效用与隐私的权衡是平衡的，匿名数据集的安全性可能依赖于许多难以控制的外部因素。为了说明这一点，我将向你展示一种叫做“链接攻击”的例子，通过这种攻击，敌人利用匿名数据之外的知识来破解数据。

这一特定攻击始于一位分析师通过纽约市自由信息法获取了纽约市所有出租车的[数据](http://www.nyc.gov/html/tlc/html/about/trip_record_data.shtml)，时间范围为某一特定时期。这些数据包括接送地点、接送时间、费用和小费金额。乍一看，这些数据本身并没有引起太多隐私警告，这也是为什么纽约最初会释放这些数据。但后来一位西北大学的研究生利用时间戳的名人登上出租车的照片，在公开的数据中找到特定的出租车行程。这意味着他可以确定某位名人给司机的小费多少，使得原本被认为是匿名的数据突然成为了新闻素材。

Gawker 报道了这个故事，并发布了一篇[文章](http://gawker.com/the-public-nyc-taxicab-database-that-accidentally-track-1646724546)，揭露了贾德·阿帕图和其他一些名人的小费习惯。我在下面重现了这一链接攻击。

贾德·阿帕图及其妻子、演员莱斯莉·曼的照片和他们旅行的地图都出现在原始的 Gawker[报道](http://gawker.com/the-public-nyc-taxicab-database-that-accidentally-track-1646724546)中：

![阿帕图](img/2d92967f0b361c27a3b697936523d910.png)

图片来源：Gawker

我们可以通过查询接送的时间戳和地点，轻松在公开的数据中找到这次旅行：

```py
SELECT pickup_datetime, dropoff_datetime, tip_amount 
FROM nyc_taxi 
WHERE pickup_datetime >= '2013-06-21 11:28:00' and pickup_datetime < '2013-06-21 11:29:00' 
AND pickup_latitude >= 40.719 and pickup_latitude <= 40.720 
AND pickup_longitude <= -74.009 and pickup_longitude >= -74.011
```

这导致了一个单独的记录，即贾德的旅行：

| **接送时间** | **下车时间** | **小费金额** |
| --- | --- | --- |
| 6/21/13 11:28 | 6/21/13 11:35 | $2.10 |

实现类似的链接攻击还有其他方法。例如，如果你有出租车收据，你可以根据收据创建的时间来使用乘车费用和下车日期/时间来发现这次旅行。值得一提的是，纽约确实尝试通过对出租车标志号码进行哈希（数据掩码技术）来使数据匿名（尽管这种尝试通过[彩虹表](https://en.wikipedia.org/wiki/Rainbow_table)也可以破解）。然而，需要注意的是，我们甚至不需要破解掩码标志号码，就可以成功地执行上述链接攻击。

### 从基数到匿名

匿名化的致命弱点在于包含最多唯一值的列，即所谓的高基数列。在利用纽约市出租车数据进行的成功链接攻击中，时间戳和位置数据被利用；由于这些列具有非常高的基数，只有一小部分接送同时发生在照片上，因此可以很容易地隔离到相同日期/时间*和*位置的单一结果。

纽约市应该如何采取不同措施来保护贾德的打赏习惯？

除了遮蔽出租车徽章外，城市还可以对该数据集应用进一步的匿名化。如果将接送时间泛化到最近的整点，那么链接攻击将会失败。我上面使用的相同查询将返回零结果，因为在那两分钟之间不会存在任何记录，因为每条记录都将被四舍五入到整点 - *我的查询对数据来说过于具体*。这是一种叫做 k-匿名化的技术。在 k-匿名化中，高基数值被泛化或“模糊化”，以尝试防止链接攻击。实际上，你可以把 k-匿名化看作是给你*更多*的结果，因为在这种情况下，我无法再查询该小时内的具体信息 - 数据变得粗糙。在这里，我们不仅仅是在保护敏感值；我们被迫保护那些有许多唯一值的列，这些列有时被称为准标识符。

不幸的是，k-匿名化并非万无一失。即使我们将数据中的接送日期/时间四舍五入以防止这种攻击，攻击者仍然可以破坏纽约市保存数据集匿名性的努力。例如，如果攻击者知道接送位置*和*放下位置，并且这两个数据点一起在该小时内唯一，这将再次破坏匿名化尝试。

这是因为接送*位置*也具有高基数。位置坐标也可以进行 k-匿名化（泛化纬度和经度）以保护匿名性，但这就是隐私与实用性权衡的体现。我们是否采取了保护隐私的措施，导致数据变得毫无用处？为了防止潜在的攻击，我们是否也阻碍了有用的分析？我们是否还需要 k-匿名化车费？这也是相当高基数的……你明白了。

![k-匿名化](img/0346681f1decfb5cd89978215f4a7ce6.png)

还有一种不同的技术称为差分隐私，它在隐私上有数学保证。你只能了解数据中的聚合趋势，并且对可以实际进行的查询数量有限制。这非常强大，因为有隐私的*保证*；然而，与 k-匿名化不同，由于查询类型和对这些查询的限制，仍然存在显著的实用性权衡。

### 谁真正关心？欧洲人。

那么这些事情与谁相关？最重要的莫过于欧洲人，他们实施了[通用数据保护条例](https://en.wikipedia.org/wiki/General_Data_Protection_Regulation)（GDPR）以保护数据主体的私人信息。违规行为可能会导致公司全球收入的 4%作为罚款。这使得 GDPR 成为全球最严肃的数据监管法规，并且适用于*任何*使用欧洲数据的业务，因此如果你是一名处理全球数据的数据科学家，你很可能会受到 GDPR 的约束。

在匿名化方面，GDPR 有一些非常模糊的指导方针（没有恶意）。让我们*深入*一些法律术语。GDPR 的序言部分是立法者对法律文本进行评论的地方。在第 26 项序言中，他们声明 GDPR“不适用于匿名信息”，匿名信息被定义为“与已识别或可识别的自然人无关的信息，或以这种方式处理的个人数据，使得数据主体无法或不再被识别。”因此，匿名化似乎是一个潜在的“免罪卡”，意味着如果一个数据集是真正匿名化的，GDPR 将不适用。

在 GDPR 的其他地方，这一匿名化的概念与伪匿名化有所区分，后者定义为“以这样的方式处理个人数据，使得这些数据不能再被归属到特定的数据主体，而无需使用额外的信息，前提是这些额外的信息被单独保管，并且采取技术和组织措施以确保这些个人数据不被归属到已识别或可识别的自然人。” 这基本上是纽约市在掩盖出租车奖章时所尝试做的事情。

根据 GDPR，匿名化数据是指“无法识别”的数据，而这些数据不受 GDPR 的监管。另一方面，伪匿名化数据则需要额外的数据来识别数据主体……这引出了一个问题：是否存在可以在提供额外信息后无法识别的数据？纽约显然认为存在这样的数据，但答案远非确定。最糟糕的情况是，可能没有 GDPR 下可接受的匿名化形式。

### 让匿名化为你服务

鉴于固有的风险，匿名化必须只是隐私保护拼图中的一部分。匿名化技术需要在更大的信息治理框架内进行，该框架可以提供匿名化能力，并根据用户的属性和当时的目的动态控制数据“状态”。这包括提供一个执行分析的环境，而不是将数据转交给第三方并失去对数据处理方式的可见性，这也是一些人用“匿名化”数据集所倾向做的事情。

那么这在实际操作中究竟意味着什么呢？这意味着没有上下文的匿名化是行不通的。更准确地说，动态数据抽象层是关键。

动态数据抽象层是一个薄层，位于所有数据之上，基于你的策略和数据呈现给消费者的方式来做出决策。这使得组织可以根据特定目的（分析上下文）或用户的某些属性限制访问权限。它还允许组织通过统一视图审计所有对数据的操作，从而生成报告，并实时了解哪些政策在何时由谁执行。最重要的是，它实际上促进了更好的数据科学，因为这个抽象层提供了一致且统一的数据视图，使得分析共享更为简便，因为数据对所有人而言来自相同的地方。

让我们回到出租车的例子，看看在实践中抽象层会是什么样的。

如果纽约能够通过数据抽象层公开他们的数据，他们将有能力将目的、用户属性和上下文与数据保护方式关联起来。例如，通过该抽象层，他们可以规定用户仅在特定目的下访问其数据。如果用户承认其目的为发现数据中的汇总趋势，那么出租车数据可以在该目的和时间点通过差分隐私进行动态保护。如果分析师随后希望分析特定位置的单个路线，位置可以保持准确，但可以对接送时间应用 k-匿名化（同样，针对该目的和时间点进行动态处理）。不仅仅是找到 Judd 的小费会破坏访问时设定的目的确认；动态匿名化加上审计可以确保这种情况不会发生。

匿名化技术可以提供隐私保障，但只有在适当工程化的情况下才能实现。隐私与实用性的权衡全在于上下文，而抽象层就是提供这种上下文的手段。如果纽约利用了这些额外的工具，名人记者可能不会太高兴。但对于那些关心数据隐私和安全的人来说，这将是一个胜利，Judd 的小费习惯也会得到保护。

**简介：[Steve Touw](https://www.linkedin.com/in/steventouw/)** 是[Immuta](https://www.immuta.com/)的联合创始人兼 CTO。Steve 拥有在美国情报界设计大规模地理时间分析的丰富经验，包括一些最早的 Hadoop 分析，以及管理复杂的多租户数据政策控制的框架。这些经验促使他和 Immuta 的联合创始人们构建了一款软件产品，旨在让数据科学团队能够访问和处理高价值数据。在加入 Immuta 之前，Steve 曾是 42six solutions 的 CTO，领导了一个大型的大数据服务工程团队，该团队被 Computer Sciences Corporation 收购。Steve 拥有马里兰大学地理学学士学位。

**相关：**

+   机器学习与人类的碰撞——来自 HUML 2016 的见解

+   Google 获取了大量关于你的数据

+   过程挖掘中的隐私、安全与伦理

### 相关主题

+   [预测未来事件：AI 与 ML 的能力与局限](https://www.kdnuggets.com/2023/06/forecasting-future-events-capabilities-limitations-ai-ml.html)

+   [Prompt Engineering 的兴起与衰落：潮流还是未来？](https://www.kdnuggets.com/the-rise-and-fall-of-prompt-engineering-fad-or-future)

+   [LLMs 的历史与未来](https://www.kdnuggets.com/history-and-future-of-llms)

+   [未来-proof 你的数据游戏：每个数据科学家在 2023 年需要掌握的顶级技能](https://www.kdnuggets.com/futureproof-your-data-game-top-skills-every-data-scientist-needs-in-2023)

+   [AI 与数据分析师：影响分析未来的 6 大局限](https://www.kdnuggets.com/ai-vs-data-analysts-top-6-limitations-impacting-the-future-of-analytics)

+   [聊天机器人变革：从失败到未来](https://www.kdnuggets.com/2021/12/chatbot-transformation-failure-future.html)
