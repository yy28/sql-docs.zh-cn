---
title: 教程：在 Python 中部署群集模型
description: 在此四部分的系列教程的第四部分中，你将在 Python 中使用 SQL Server 机器学习服务部署群集模型。
ms.prod: sql
ms.technology: machine-learning
ms.devlang: python
ms.date: 08/27/2019
ms.topic: tutorial
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 923fae2a6b215814888b04dc674b67e4c87bc00d
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70238690"
---
# <a name="tutorial-deploy-a-clustering-model-in-python-with-sql-server-machine-learning-services"></a>教程：使用 SQL Server 机器学习服务在 Python 中部署群集模型

在此四部分的系列教程的第四部分中，你将使用 SQL Server 机器学习服务将 Python 中开发的聚类分析模型部署到 SQL 数据库。

为了定期执行群集，在新客户注册时，需要能够从任何应用调用 Python 脚本。 为此，你可以通过将 Python 脚本放在数据库中的 SQL 存储过程中，在 SQL Server 中部署 Python 脚本。 因为模型在 SQL 数据库中执行，所以可以轻松地对数据库中存储的数据进行定型。

在本部分中，你会将刚刚编写的 Python 代码移到 SQL Server 并通过 SQL Server 机器学习服务的帮助部署群集。

本文将介绍如何执行以下操作：

> [!div class="checklist"]
> * 创建用于生成模型的存储过程
> * 在 SQL Server 中执行群集
> * 使用聚类分析信息

在[第一部分](tutorial-python-clustering-model.md)中，你安装了必备组件，并导入了示例数据库。

[第二部分](tutorial-python-clustering-model-prepare-data.md)介绍了如何从 SQL 数据库准备要执行群集的数据。

第[三部分](tutorial-python-clustering-model-build.md)介绍了如何在 Python 中创建和训练 K 平均值聚类分析模型。

## <a name="prerequisites"></a>先决条件

* 本系列教程的第四部分假设你满足了[**第一部分**](tutorial-python-clustering-model.md)的先决条件，并完成了[**第二**](tutorial-python-clustering-model-prepare-data.md)部分和[**第三**](tutorial-python-clustering-model-build.md)部分中的步骤。

## <a name="create-a-stored-procedure-that-generates-the-model"></a>创建用于生成模型的存储过程

运行以下 T-sql 脚本来创建存储过程。 此过程将重新创建在本教程系列的第一部分和第二部分中开发的步骤：

* 根据客户的购买和返回历史记录对客户进行分类
* 使用 K 平均值算法生成四个客户群集

```sql
USE [tpcxbb_1gb]
GO

CREATE procedure [dbo].[py_generate_customer_return_clusters]
AS

BEGIN
    DECLARE

-- Input query to generate the purchase history & return metrics
     @input_query NVARCHAR(MAX) = N'
SELECT
  ss_customer_sk AS customer,
  CAST( (ROUND(COALESCE(returns_count / NULLIF(1.0*orders_count, 0), 0), 7) ) AS FLOAT) AS orderRatio,
  CAST( (ROUND(COALESCE(returns_items / NULLIF(1.0*orders_items, 0), 0), 7) ) AS FLOAT) AS itemsRatio,
  CAST( (ROUND(COALESCE(returns_money / NULLIF(1.0*orders_money, 0), 0), 7) ) AS FLOAT) AS monetaryRatio,
  CAST( (COALESCE(returns_count, 0)) AS FLOAT) AS frequency
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
    GROUP BY sr_customer_sk
  ) returned ON ss_customer_sk=sr_customer_sk
 '

EXEC sp_execute_external_script
      @language = N'Python'
    , @script = N'

import pandas as pd
from sklearn.cluster import KMeans

#get data from input query
customer_data = my_input_data

#We concluded in step 2 in the tutorial that 4 would be a good number of clusters
n_clusters = 4

#Perform clustering
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orderRatio","itemsRatio","monetaryRatio","frequency"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
    , @input_data_1 = @input_query
    , @input_data_1_name = N'my_input_data'
             with result sets (("Customer" int, "orderRatio" float,"itemsRatio" float,"monetaryRatio" float,"frequency" float,"cluster" float));
END;
GO
```

## <a name="perform-clustering-in-sql-database"></a>在 SQL 数据库中执行群集

现在，你已创建了存储过程，请执行以下脚本，以使用该过程执行群集操作。

```sql
--Create a table to store the predictions in

DROP TABLE IF EXISTS [dbo].[py_customer_clusters];
GO

CREATE TABLE [dbo].[py_customer_clusters] (
    [Customer] [bigint] NULL
  , [OrderRatio] [float] NULL
  , [itemsRatio] [float] NULL
  , [monetaryRatio] [float] NULL
  , [frequency] [float] NULL
  , [cluster] [int] NULL
  ,
    ) ON [PRIMARY]
GO

--Execute the clustering and insert results into table
INSERT INTO py_customer_clusters
EXEC [dbo].[py_generate_customer_return_clusters];

-- Select contents of the table to verify it works
SELECT * FROM py_customer_clusters;
```

## <a name="use-the-clustering-information"></a>使用聚类分析信息

因为你在数据库中存储了聚类分析过程，所以它可以针对存储在同一数据库中的客户数据有效地执行群集操作。 每当更新客户数据并使用更新的群集信息时，就可以执行该过程。

假设你想要向群集0中的客户发送促销电子邮件，此组处于非活动状态（你可以在本教程的第[三部分](tutorial-python-clustering-model-build.md#analyze-the-results)中了解这四个分类的描述）。 以下代码选择群集0中的客户的电子邮件地址。

```sql
USE [tpcxbb_1gb]
--Get email addresses of customers in cluster 0 for a promotion campaign
SELECT customer.[c_email_address], customer.c_customer_sk
  FROM dbo.customer
  JOIN
  [dbo].[py_customer_clusters] as c
  ON c.Customer = customer.c_customer_sk
  WHERE c.cluster = 0
```

您可以更改**c 群集**值，以返回其他分类中的客户的电子邮件地址。

## <a name="clean-up-resources"></a>清理资源

完成本教程后，可以从 SQL Server 中删除 tpcxbb_1gb 数据库。

## <a name="next-steps"></a>后续步骤

本系列教程的第四部分已完成以下步骤：

* 创建用于生成模型的存储过程
* 在 SQL Server 中执行群集
* 使用聚类分析信息

若要了解有关在 SQL Server 机器学习服务中使用 Python 的详细信息，请参阅：

* [快速入门：在 SQL Server 上运行 "Hello world" Python 脚本机器学习服务](quickstart-python-run-using-t-sql.md)
* [适用于 SQL Server 机器学习服务的其他 Python 教程](sql-server-python-tutorials.md)
* [通过 sqlmlutils 安装 Python 包](../package-management/install-additional-python-packages-on-sql-server.md)

