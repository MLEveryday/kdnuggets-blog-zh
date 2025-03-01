# 我的训练数据和测试数据有多（不）相似？

> 原文：[`www.kdnuggets.com/2018/06/how-dissimilar-train-test-data.html`](https://www.kdnuggets.com/2018/06/how-dissimilar-train-test-data.html)

![c](img/3d9c022da2d331bb56691a9617b91b90.png) 评论

**由 [Shikhar Gupta](https://twitter.com/shik1470) 提供**

人们总是说不要拿苹果和橘子做比较。但是如果我们比较的是一组苹果和橘子的混合与另一组苹果和橘子的混合，但分布不同，那你还能比较吗？你将如何进行比较呢？

* * *

## 我们的三大课程推荐

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 1\. [谷歌网络安全证书](https://www.kdnuggets.com/google-cybersecurity) - 快速进入网络安全职业生涯。

![](img/e225c49c3c91745821c8c0368bf04711.png) 2\. [谷歌数据分析专业证书](https://www.kdnuggets.com/google-data-analytics) - 提升你的数据分析能力

![](img/0244c01ba9267c002ef39d4907e0b8fb.png) 3\. [谷歌 IT 支持专业证书](https://www.kdnuggets.com/google-itsupport) - 在 IT 领域支持你的组织

* * *

在现实世界的大多数情况下，你会遇到后一种情况。

![](img/7fd101b721fb668c1c84bbdb733785ce.png)

这在数据科学中发生得很频繁。在开发机器学习模型时，我们会遇到一种情况，即我们的模型在训练数据上表现良好，但在测试数据上却无法达到相同的性能。

我这里不是在谈论过拟合。即使我根据交叉验证选择了最好的模型，并且它在测试数据上表现仍然很差，那么测试数据中存在一些我们未能捕捉到的内在模式。< 想象一个我试图建模顾客购物行为的情况。如果我的训练数据和测试数据如下图所示，你可以清楚地看到这个问题。 ![](img/43e718e8ed8f3f92c83ced1e95a27790.png)

> 模型将基于与测试数据相比平均年龄较低的客户进行训练。这个模型从未见过测试数据中那种年龄模式。如果年龄在你的模型中是一个重要特征，那么它在测试数据上表现会很差。

在这篇文章中，我将讨论如何识别这个问题以及一些解决方案的初步想法。

### 协变量漂移

我们可以更正式地定义这种情况。**协变量**指的是我们模型中的预测变量。**协变量漂移**指的是预测变量在训练数据和测试数据中具有不同的**特征（分布）**的情况。

在具有许多变量的现实世界问题中，协变量漂移很难被发现。在这篇文章中，我尝试讨论一种识别这种情况的方法，以及如何考虑训练数据和测试数据之间的这种漂移。

### 基本概念

> 如果存在协变量漂移，那么在混合训练集和测试集后，我们仍然能够以较高的准确率对每个数据点的来源（是来自测试集还是训练集）进行分类。

![](img/5fffdd4138a36a820dde11d61ba677df.png)

让我们深入理解一下。考虑上述例子，其中年龄是测试和训练之间的漂移特征。如果我们使用随机森林等分类器来将行分类为测试和训练，年龄将成为数据拆分中的一个非常重要的特征。

![](img/b84dfc6b3d7271b626a6a088a6d0dbfd.png)

### 实施

现在，让我们尝试将这个想法应用于实际数据集。我使用的是来自这个 Kaggle 竞赛的数据集：[`www.kaggle.com/c/porto-seguro-safe-driver-prediction/data`](https://www.kaggle.com/c/porto-seguro-safe-driver-prediction/data)

*步骤 1：数据预处理*

我们首先需要清理数据，填补所有缺失值，并对所有分类变量进行标签编码。对于这个数据集，这一步骤并不需要，因此我跳过了这一步。

```py
#loading test and train data
train = pd.read_csv(‘train.csv’,low_memory=True)
test = pd.read_csv(‘test.csv’,low_memory=True)
```

*步骤 2：*

我们需要在训练和测试数据中都添加一个特征**‘is_train’**。这个特征的值将是**测试集为 0，训练集为 1**。

```py
#adding a column to identify whether a row comes from train or not
test[‘is_train’] = 0
train[‘is_train’] = 1 
```

*合并训练和测试*

然后我们需要将两个数据集合并。**此外，由于训练数据中有原始的‘target’变量，而测试数据中没有，所以我们也必须丢弃那个变量。**

**注意：** 对于你的问题，‘target’将被替换为原始问题中因变量的名称。

```py
#combining test and train data
df_combine = pd.concat([train, test], axis=0, ignore_index=True)
#dropping ‘target’ column as it is not present in the test
df_combine = df_combine.drop(‘target’, axis =1)
```

```py
y = df_combine['is_train'].values #labels
x = df_combine.drop('is_train', axis=1).values #covariates or our independent variables
```

```py
tst, trn = test.values, train.values
```

*步骤 4：构建和测试分类器*

为了分类目的，我使用**随机森林分类器**来预测合并数据集中每一行的标签。你也可以使用其他任何分类器。

```py
m = RandomForestClassifier(n_jobs=-1, max_depth=5, min_samples_leaf = 5)
predictions = np.zeros(y.shape) #creating an empty prediction array
```

我们使用分层 4 折来确保每个类别的百分比得到保留，并且覆盖整个数据集。对于每一行，分类器将计算其属于训练集的概率。

```py
skf = SKF(n_splits=20, shuffle=True, random_state=100)
for fold, (train_idx, test_idx) in enumerate(skf.split(x, y)):
 X_train, X_test = x[train_idx], x[test_idx]
 y_train, y_test = y[train_idx], y[test_idx]

 m.fit(X_train, y_train)
 probs = m.predict_proba(X_test)[:, 1] #calculating the probability
 predictions[test_idx] = probs
```

*步骤 5：解释结果*

我们将输出分类器的 ROC-AUC 指标，以估算数据的协变量偏移程度。

> 如果分类器能够以良好的准确性将行分类为训练和测试，我们的 AUC 分数应该较高（大于 0.8）。这意味着训练和测试之间存在强烈的协变量偏移。

```py
print(‘ROC-AUC for train and test distributions:’, AUC(y, predictions))
```

```py
# ROC-AUC for train and test distributions: 0.49944573868
```

> AUC 值为 0.49 意味着没有强烈的协变量偏移证据。这意味着大多数观察结果来自一个不特定于测试或训练的特征空间。

由于这个数据集来自 Kaggle，所以这个结果是相当预期的。在这种竞赛数据集中，数据通常经过精心策划，以确保没有这样的偏移。

这个过程可以在任何数据科学问题中复制，以检查在开始建模之前是否存在协变量偏移。

### 超越

此时我们要么观察到协变量偏移，要么没有。那么我们可以做些什么来提高测试数据上的性能呢？

1.  丢弃漂移特征

1.  使用密度比估计进行重要性加权

**丢弃漂移特征：**

**注意：** 这种方法适用于你观察到协变量偏移的情况。

+   从我们在上一节中构建的随机森林分类器对象中提取特征重要性

+   顶级特征是那些正在漂移并导致转移的特征。

+   从最重要的特征中一次删除一个变量，构建你的模型并检查其性能。收集所有那些性能没有下降的特征。

+   在构建最终模型时，现在删除所有这些特征。

![](img/4f8f24d188f813f569030fe34a3240aa.png)

> 这个想法是去除那些落在红色桶中的特征。

**使用密度比估计的重要性权重**

**注意：** 该方法适用于是否存在协变量转移的情况。

让我们看看我们在上一节中计算的预测结果。对于每个观察值，这个预测结果告诉我们它属于训练数据的概率。

```py
predictions[:10]
----output-----
```

```py
array([ 0.34593171])
```

所以对于第一行，我们的分类器认为它以.34 的概率属于训练数据。我们称之为 P(train)。或者我们也可以说它有.66 的概率来自测试数据。我们称之为 P(test)。现在这里是魔法技巧：

对于每一行训练数据，我们计算一个系数**w = P(test)/P(train)**。

这个 w 告诉我们观察值与训练数据的接近程度。这里是重点：

> 我们可以将这个 w 作为任何分类器中的样本权重，以增加这些与测试数据相似的观察值的权重。直观上，这很有意义，因为我们的模型将更多关注于捕捉那些与测试数据相似的观察值中的模式。

这些权重可以使用以下代码计算。

```py
plt.figure(figsize=(20,5))
predictions_train = predictions[len(tst):] #filtering the actual training rows
weights = (1./predictions_train) — 1\. 
weights /= np.mean(weights) # Normalizing the weights
```

```py
plt.xlabel(‘Computed sample weight’)
plt.ylabel(‘# Samples’)
sns.distplot(weights, kde=False)
```

< 你可以像这样将模型拟合方法中计算的权重传递进去：

```py
m = RandomForestClassifier(n_jobs=-1,max_depth=5)
```

```py
m.fit(X_train, y_train, *sample_weight=weights*)
```

![](img/4781dc6afd070dbf42e7978dbc01e0f6.png)

在上述图中需要注意的一些事项：

+   观察值的权重越高，它与测试数据的相似性就越大。

+   几乎 70%的训练样本的样本权重接近 1，因此来自于一个对训练或测试高密度区域不是非常特定的特征空间。这与我们计算的 AUC 值一致。

### 结束语

我希望现在你对协变量转移有了更好的理解，知道如何识别并有效处理它。

**简介：[Shikhar Gupta](https://twitter.com/shik1470)** 正在旧金山大学攻读数据科学硕士学位，实习于@IsaziConsulting，@iitroorkee 校友。

[原文](https://towardsdatascience.com/how-dis-similar-are-my-train-and-test-data-56af3923de9b)。转载获得许可。

**相关：**

+   [训练集、测试集和 10 折交叉验证](https://www.kdnuggets.com/2018/01/training-test-sets-cross-validation.html)

+   [开源数据科学/机器学习生态系统的 6 个组成部分；Python 是否战胜了 R？](https://www.kdnuggets.com/2018/06/ecosystem-data-science-python-victory.html)

+   [帮派暴力的统计数据](https://www.kdnuggets.com/2018/06/statistics-gang-violence.html)

### 更多相关内容

+   [如何通过使用自动 EDA 工具在数据科学评估测试中脱颖而出](https://www.kdnuggets.com/2022/04/ace-data-science-assessment-test-automatic-eda-tools.html)

+   [在 Python 中执行 T 检验](https://www.kdnuggets.com/2023/01/performing-ttest-python.html)

+   [超越准确性：使用 NLP 测试库评估和改进模型](https://www.kdnuggets.com/2023/04/john-snow-beyond-accuracy-nlp-test-library.html)

+   [如何从零开始构建和训练 Transformer 模型…](https://www.kdnuggets.com/how-to-build-and-train-a-transformer-model-from-scratch-with-hugging-face-transformers)

+   [为什么我们总是需要人类来训练 AI — 有时需要实时进行](https://www.kdnuggets.com/2021/12/why-we-need-humans-training-ai.html)

+   [使用 Tensorflow 训练图像分类模型指南](https://www.kdnuggets.com/2022/12/guide-train-image-classification-model-tensorflow.html)
