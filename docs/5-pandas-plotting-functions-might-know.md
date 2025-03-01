# 5 个你可能不知道的 Pandas 绘图函数

> 原文：[`www.kdnuggets.com/2023/02/5-pandas-plotting-functions-might-know.html`](https://www.kdnuggets.com/2023/02/5-pandas-plotting-functions-might-know.html)

![5 Pandas Plotting Functions You Might Not Know](img/d453a8c95f228803ff5127333f865ade.png)

图片由[rawpixel.com](https://www.freepik.com/free-vector/illustration-data-analysis-graph_2807755.htm#query=data%20science&position=4&from_view=search&track)提供，[Freepik](https://www.freepik.com/)上的图片。

Pandas 是一个著名的数据处理包，许多人使用它。它之所以著名，是因为它直观且易于使用。此外，Pandas 得到了社区的广泛支持，以增强该包。

* * *

## 我们的前三个课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [Google Cybersecurity Certificate](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [Google Data Analytics Professional Certificate](https://www.kdnuggets.com/google-data-analytics) - 提升您的数据分析技能

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [Google IT Support Professional Certificate](https://www.kdnuggets.com/google-itsupport) - 在 IT 领域支持您的组织

* * *

然而，只有少数人知道 Pandas 也有绘图函数。Pandas 的一些绘图函数非常特别，并且为您的数据分析提供了洞察力。这些函数是什么？让我们一起探索。

对于我们的示例，我们将使用商业上可用的[Titanic Data from Kaggle](https://www.kaggle.com/c/titanic)。

# Bootstrap 图

Bootstrap 图是 Pandas 中的一个绘图函数，通过使用自助法函数（数据采样带替换）来估计统计不确定性。当测量数据统计（均值、中位数、范围）并进行区间估计时，这是一个快速的绘图函数。

让我们尝试使用这个函数与数据样本。

```py
import pandas as pd

df = pd.read_csv('train.csv')
pd.plotting.bootstrap_plot(df['Fare'], size = 150, samples = 1000)
```

![5 Pandas Plotting Functions You Might Not Know](img/72c7889da87bc7a4e797c5335f718e4f.png)

该图将根据样本参数的大小重新采样数据。

均值的分布估计接近 30 到 40，中位数接近 12 到 15。通过这个图，我们可以尝试估计实际的人口统计数据。由于采样是随机的，您的结果可能与我的不同。

# Scatter Matrix 图

Scatter Matrix 图是 Pandas 中的一个绘图函数，用于从所有可用的数值数据中创建散点图。让我们尝试这个函数，了解散点矩阵。

```py
pd.plotting.scatter_matrix(df)
```

![5 Pandas Plotting Functions You Might Not Know](img/daa847afc6b3df6a049fab5364a6eeed.png)

如上图所示，散点矩阵函数自动检测数据框中的所有数值列，并为每个组合创建散点矩阵。该函数为相同列创建直方图以测量数据分布。

# Radviz 图

Radviz 图是一种将 N 维数据可视化为 2D 图的图表。通常，具有超过 3 个维度的数据很难可视化，但我们可以使用 Radviz 图做到这一点。让我们用数据示例来尝试一下。

```py
pd.plotting.radviz(df[['SibSp', 'Parch', 'Pclass', 'Age', 'Fare','Survived']], 'Survived', color =['blue', 'red'])
```

![你可能不知道的 5 个 Pandas 绘图函数](img/6c2557f5f464052b7c40f960f94987d3.png)

在上述函数中，我们仅使用了带有目标的数值数据来划分数据。

结果如上图所示。然而，我们如何解释上述图表？对于每个变量，它将被均匀地表示为一个圆圈。每个变量中的数据点将根据其值被绘制在圆圈内。高度相关的变量将在圆圈中更靠近，而低相关的变量则会较远。

# Andrew 曲线图

Andrew 曲线绘图是一种可视化多变量数据的方法，以潜在地识别数据中的聚类。它也可以用于识别数据中是否存在任何分离。让我们用数据示例来尝试一下。

Andrew 曲线在数据标准化到 0 到 1 之间时效果最佳，因此我们在应用函数之前会预处理数据。

```py
from sklearn.preprocessing import MinMaxScaler

df = df.drop(['PassengerId', 'Name', 'Sex', 'Ticket', 'Cabin', 'Embarked'], axis =1)
scaler = MinMaxScaler()
df_scaled = scaler.fit_transform(df.drop('Survived', axis =1))

df_scaled = pd.DataFrame(df_scaled, columns = df.drop('Survived', axis =1).columns)
df_scaled['Survived'] = df['Survived']

pd.plotting.andrews_curves(df_scaled, 'Survived', color =['blue', 'red'])
```

![你可能不知道的 5 个 Pandas 绘图函数](img/a5f8bcf13723412c9be7c0c332407dcb.png)

从上面的图像中，我们可以看到“生存”类别可能具有不同的聚类。

# 延迟图

延迟图是一个特定的时间序列数据图，用于检查时间序列数据是否与自身相关以及是否随机。延迟图通过将时间数据与其延迟数据进行绘图来工作。例如，延迟 1 的 T1 数据将是 T1 与 T1+1（或 T2）数据的绘图。让我们尝试这些函数以更好地理解。

我们将为这个示例创建样本时间序列数据。

```py
np.random.seed(34)
x = np.cumsum(np.random.normal(loc=1, scale=5, size=100))
s = pd.Series(x)
s.plot()
```

![你可能不知道的 5 个 Pandas 绘图函数](img/25bedb939a7c37dadcd7ae2d837867e6.png)

我们可以看到我们的时间序列数据显示出递增模式。让我们看看使用延迟图时它的表现。

```py
pd.plotting.lag_plot(s, lag=1)
```

![你可能不知道的 5 个 Pandas 绘图函数](img/f43d4b747531aefb238818adb47b709f.png)

当我们使用延迟 1 的延迟图时，我们可以看到数据表现出线性模式。这意味着数据在 1 天差异上存在自相关。让我们看看使用按月的情况是否存在相关性。

```py
pd.plotting.lag_plot(s, lag=30)
```

![你可能不知道的 5 个 Pandas 绘图函数](img/2ce4ba88a9513980efd6c85a4726547f.png)

现在数据变得稍微随机一些，尽管仍然存在线性模式。

# 结论

Pandas 是一个数据处理包，还提供了各种独特的绘图函数。在这篇文章中，我们讨论了 5 种不同的 Pandas 绘图函数：

1.  自助绘图

1.  散点矩阵图

1.  Radviz 图

1.  Andrew 曲线图

1.  延迟图

**[Cornellius Yudha Wijaya](https://www.linkedin.com/in/cornellius-yudha-wijaya/)** 是数据科学助理经理和数据撰写员。在全职工作于 Allianz Indonesia 的同时，他喜欢通过社交媒体和写作媒体分享 Python 和数据技巧。

### 更多相关主题

+   [7 个 Pandas 绘图函数用于快速数据可视化](https://www.kdnuggets.com/7-pandas-plotting-functions-for-quick-data-visualization)

+   [你下次面试可能会遇到的 24 个 SQL 问题](https://www.kdnuggets.com/2022/06/24-sql-questions-might-see-next-interview.html)

+   [数据科学中的绘图与数据可视化](https://www.kdnuggets.com/2022/06/plotting-data-visualization-data-science.html)

+   [每个数据科学家都应该知道的 10 个 Pandas 函数](https://www.kdnuggets.com/10-essential-pandas-functions-every-data-scientist-should-know)

+   [数据科学面试中你应该知道的五大 SQL 窗口函数](https://www.kdnuggets.com/2022/01/top-five-sql-window-functions-know-data-science-interviews.html)

+   [4 个你可能不知道的 Python Itertools 过滤函数](https://www.kdnuggets.com/2023/08/4-python-itertools-filter-functions-probably-didnt-know.html)
