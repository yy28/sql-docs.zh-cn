---
title: 教程：在 Python 中生成聚类分析模型
description: 在这四个部分的系列教程的第三部分中，你将构建一个 K 平均值的模型，以便在 Python 中使用 SQL Server 机器学习服务执行群集。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e768f213edf27528e38b2f18d719869fbf089f21
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238707"
---
# <a name="tutorial-build-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>教程：使用 SQL Server 机器学习服务在 Python 中生成聚类分析模型

在这四个部分的系列教程的第三部分中，你将在 Python 中构建一个 K 平均值的模型来执行聚类分析。 在本系列的下一部分中，你将在 SQL 数据库中使用 SQL Server 机器学习服务部署此模型。

本文将介绍如何执行以下操作：

> [!div class="checklist"]
> * 定义 K 平均值算法的分类数
> * 执行群集
> * 分析结果

在[第一部分](tutorial-python-clustering-model.md)中，你安装了必备组件，并导入了示例数据库。

[第二部分](tutorial-python-clustering-model-prepare-data.md)介绍了如何从 SQL 数据库准备要执行群集的数据。

在[第四部分](tutorial-python-clustering-model-deploy.md)中，你将了解如何在 SQL 数据库中创建一个存储过程，该存储过程可基于新数据在 Python 中执行群集操作。

## <a name="prerequisites"></a>先决条件

* 本教程的第三部分假设你满足了[**第一部分**](tutorial-python-clustering-model.md)的先决条件，并完成了[**第二部分**](tutorial-python-clustering-model-prepare-data.md)中的步骤。

## <a name="define-the-number-of-clusters"></a>定义群集数量

若要对你的客户数据进行分类，你将使用**K 平均值**聚类算法，这是对数据进行分组的最简单、最常见的方法之一。
有关 k 平均值的详细信息，请参阅[k 平均值聚类分析算法](https://www.kdnuggets.com/2019/05/guide-k-means-clustering-algorithm.html)。

该算法接受两个输入：数据本身和预定义的数字 "*k*"，表示要生成的分类数。
输出是*k*群集，其中输入数据已在群集中分区。

K 平均值的目标是将各项分组到 k 个分类中，以便同一群集中的所有项彼此相似，并与其他群集中的项不同。

若要确定要使用的算法的分类数，请使用中的组内方差，按提取的分类数。 要使用的相应分类数位于绘图的弯曲或 "肘形" 中。

```python
################################################################################################
## Determine number of clusters using the Elbow method
################################################################################################

cdata = customer_data
K = range(1, 20)
KM = (sk_cluster.KMeans(n_clusters=k).fit(cdata) for k in K)
centroids = (k.cluster_centers_ for k in KM)

D_k = (sci_distance.cdist(cdata, cent, 'euclidean') for cent in centroids)
dist = (np.min(D, axis=1) for D in D_k)
avgWithinSS = [sum(d) / cdata.shape[0] for d in dist]
plt.plot(K, avgWithinSS, 'b*-')
plt.grid(True)
plt.xlabel('Number of clusters')
plt.ylabel('Average within-cluster sum of squares')
plt.title('Elbow for KMeans clustering')
plt.show()
```

![肘形图](./media/python-tutorial-elbow-graph.png)

根据图形，其外观类似于*k = 4* ，这是一个很好的尝试值。 这*k*值会将客户分组为四个分类。

## <a name="perform-clustering"></a>执行群集

在下面的 Python 脚本中，你将使用 spark-sklearn 包中的 KMeans 函数。

```python
################################################################################################
## Perform clustering using Kmeans
################################################################################################

# It looks like k=4 is a good number to use based on the elbow graph.
n_clusters = 4

means_cluster = sk_cluster.KMeans(n_clusters=n_clusters, random_state=111)
columns = ["orderRatio", "itemsRatio", "monetaryRatio", "frequency"]
est = means_cluster.fit(customer_data[columns])
clusters = est.labels_
customer_data['cluster'] = clusters

# Print some data about the clusters:

# For each cluster, count the members.
for c in range(n_clusters):
    cluster_members=customer_data[customer_data['cluster'] == c][:]
    print('Cluster{}(n={}):'.format(c, len(cluster_members)))
    print('-'* 17)
print(customer_data.groupby(['cluster']).mean())
```

## <a name="analyze-the-results"></a>分析结果

现在，你已使用 K 平均值执行了聚类分析，下一步是分析结果，并查看是否可以找到任何可操作的信息。

查看从上一脚本打印的聚类分析平均值和群集大小。

```results
Cluster0(n=31675):
-------------------
Cluster1(n=4989):
-------------------
Cluster2(n=1):
-------------------
Cluster3(n=671):
-------------------

         customer  orderRatio  itemsRatio  monetaryRatio  frequency
cluster
0        50854.809882    0.000000    0.000000       0.000000   0.000000
1        51332.535779    0.721604    0.453365       0.307721   1.097815
2        57044.000000    1.000000    2.000000     108.719154   1.000000
3        48516.023845    0.136277    0.078346       0.044497   4.271237
```

这四个分类是使用[第一部分](tutorial-python-clustering-model-prepare-data.md#separate-customers)中定义的变量指定的：

* *orderRatio* = 返回订单比率（部分或全部返回的订单总数与订单总数相同）
* *itemsRatio* = 返回项的比率（返回的项总数与购买的项数）
* *monetaryRatio* = 返回金额比率（返回的项目的总货币金额与购买的金额）
* *frequency* = 返回频率

使用 K 平均值的数据挖掘通常需要进一步分析结果，并执行更多步骤来更好地了解每个分类，但它可以提供一些优秀的潜在顾客。
可以通过以下几种方法解释这些结果：

* 群集0似乎是一组未处于活动状态的客户（所有值均为零）。
* 群集3似乎是一个在返回行为方面出现的组。

群集0是一组清晰不活跃的客户。 也许你可以将市场营销活动定向到此组，以触发对购买的兴趣。 在下一步中，你将在数据库中查询群集0中的客户的电子邮件地址，以便向他们发送市场营销电子邮件。

## <a name="clean-up-resources"></a>清理资源

如果不打算继续学习本教程，请从 SQL Server 中删除 tpcxbb_1gb 数据库。

## <a name="next-steps"></a>后续步骤

在本系列教程的第三部分中，你已完成以下步骤：

* 定义 K 平均值算法的分类数
* 执行群集
* 分析结果

若要部署已创建的机器学习模型，请遵循本系列教程中的第四部分：

> [!div class="nextstepaction"]
> [教程：使用 SQL Server 机器学习服务在 Python 中部署群集模型](tutorial-python-clustering-model-deploy.md)