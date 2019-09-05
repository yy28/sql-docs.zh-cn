---
title: 教程：准备数据以对 Python 中的客户进行分类
description: 在此四部分的系列教程的第二部分中，你将从 SQL Server 数据库中准备数据，以便在 Python 中使用 SQL Server 机器学习服务执行群集。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/30/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d91f3b9f1e3d1abe53d677d9f9058058d321d985
ms.sourcegitcommit: 26715b4dbef95d99abf2ab7198a00e6e2c550243
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70294342"
---
# <a name="tutorial-prepare-data-to-categorize-customers-in-python-with-sql-server-machine-learning-services"></a>教程：准备数据以将 Python 中的客户分类 SQL Server 机器学习服务

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此四部分的系列教程的第二部分中，将使用 Python 从 SQL 数据库还原和准备数据。 稍后在本系列中，你将使用此数据，通过 SQL Server 机器学习服务在 Python 中训练和部署群集模型。

本文将介绍如何执行以下操作：

> [!div class="checklist"]
> * 使用 Python 将不同维度中的客户隔开
> * 将数据从 SQL 数据库加载到 Python 数据帧中

在[第一部分](python-clustering-model.md)中，你安装了必备组件并还原了示例数据库。

在[第三部分](python-clustering-model-build.md)中，你将了解如何在 Python 中创建和训练 K 平均值聚类分析模型。

在[第四部分](python-clustering-model-deploy.md)中，你将了解如何在 SQL 数据库中创建一个存储过程，该存储过程可基于新数据在 Python 中执行群集操作。

## <a name="prerequisites"></a>先决条件

* 本教程的第二部分假设已满足[**第一部分**](python-clustering-model.md)的先决条件。

## <a name="separate-customers"></a>单独的客户

若要为客户群集做好准备，首先要将客户划分为以下维度：

* **orderRatio** = 返回订单比率（部分或全部返回的订单总数与订单总数相同）
* **itemsRatio** = 返回项的比率（返回的项总数与购买的项数）
* **monetaryRatio** = 返回金额比率（返回的项目的总货币金额与购买的金额）
* **frequency** = 返回频率

在 Azure Data Studio 中打开一个新笔记本，然后输入以下脚本。

在连接字符串中，根据需要替换连接详细信息。

```python
# Load packages.
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import revoscalepy as revoscale
from scipy.spatial import distance as sci_distance
from sklearn import cluster as sk_cluster

################################################################################################

## Connect to DB and select data

################################################################################################

# Connection string to connect to SQL Server named instance.
conn_str = 'Driver=SQL Server;Server=localhost;Database=tpcxbb_1gb;Trusted_Connection=True;'

input_query = '''SELECT
ss_customer_sk AS customer,
ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) AS orderRatio,
ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) AS itemsRatio,
ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) AS monetaryRatio,
COALESCE(returns_count, 0) AS frequency
FROM
(
  SELECT
    ss_customer_sk,
    -- return order ratio
    COUNT(distinct(ss_ticket_number)) AS orders_count,
    -- return ss_item_sk ratio
    COUNT(ss_item_sk) AS orders_items,
    -- return monetary amount ratio
    SUM( ss_net_paid ) AS orders_money
  FROM store_sales s
  GROUP BY ss_customer_sk
) orders
LEFT OUTER JOIN
(
  SELECT
    sr_customer_sk,
    -- return order ratio
    count(distinct(sr_ticket_number)) as returns_count,
    -- return ss_item_sk ratio
    COUNT(sr_item_sk) as returns_items,
    -- return monetary amount ratio
    SUM( sr_return_amt ) AS returns_money
FROM store_returns
GROUP BY sr_customer_sk ) returned ON ss_customer_sk=sr_customer_sk'''


# Define the columns we wish to import.
column_info = {
    "customer": {"type": "integer"},
    "orderRatio": {"type": "integer"},
    "itemsRatio": {"type": "integer"},
    "frequency": {"type": "integer"}
}
```

## <a name="load-the-data-into-a-data-frame"></a>将数据加载到数据帧中

查询的结果将使用 revoscalepy **RxSqlServerData**函数返回到 Python。 在此过程中，您将使用在前面的脚本中定义的列信息。

```python
data_source = revoscale.RxSqlServerData(sql_query=input_query, column_Info=column_info,
                                        connection_string=conn_str)
revoscale.RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)
# import data source and convert to pandas dataframe.
customer_data = pd.DataFrame(revoscale.rx_import(data_source))
```

现在显示数据帧的开头，验证其外观是否正确。

```python
print("Data frame:", customer_data.head(n=5))
```

```results
Rows Read: 37336, Total Rows Processed: 37336, Total Chunk Time: 0.172 seconds
Data frame:     customer  orderRatio  itemsRatio  monetaryRatio  frequency
0    29727.0    0.000000    0.000000       0.000000          0
1    97643.0    0.068182    0.078176       0.037034          3
2    57247.0    0.000000    0.000000       0.000000          0
3    32549.0    0.086957    0.068657       0.031281          4
4     2040.0    0.000000    0.000000       0.000000          0
```

## <a name="clean-up-resources"></a>清理资源

如果不打算继续学习本教程，请从 SQL Server 中删除 tpcxbb_1gb 数据库。

## <a name="next-steps"></a>后续步骤

在本系列教程的第二部分中，您完成了以下步骤：

* 使用 Python 将不同维度中的客户隔开
* 将数据从 SQL 数据库加载到 Python 数据帧中

若要创建使用此客户数据的机器学习模型，请遵循本教程系列的第三部分：

> [!div class="nextstepaction"]
> [教程：使用 SQL Server 机器学习服务在 Python 中创建预测模型](python-clustering-model-build.md)
