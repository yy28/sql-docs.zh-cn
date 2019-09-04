---
title: Python 教程：准备数据（线性回归）
description: 在本教程中，您将在 SQL Server 机器学习服务中使用 Python 和线性回归来预测滑雪租赁的数量。 你将使用 Python 从 SQL Server 数据库准备数据。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/03/2019
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c6c4d5fb4ffc5049f7e1325267b7623dc195e9d8
ms.sourcegitcommit: ecb19d0be87c38a283014dbc330adc2f1819a697
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2019
ms.locfileid: "70242495"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 教程：准备数据以在 SQL Server 中训练线性回归模型机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在此四部分的系列教程的第二部分中，你将使用 Python 从 SQL Server 数据库准备数据。 本系列稍后将使用此数据，通过 SQL Server 机器学习服务在 Python 中训练和部署线性回归模型。

本文将介绍如何执行以下操作：

> [!div class="checklist"]
> * 将 SQL Server 数据库中的数据加载到**pandas**数据帧中
> * 通过删除某些列在 Python 中准备数据

在[第一部分](python-ski-rental-linear-regression.md)中，您学习了如何还原示例数据库。

在[第三部分](python-ski-rental-linear-regression-train-model.md)中，你将了解如何在 Python 中训练线性回归机器学习模型。

在[第四部分](python-ski-rental-linear-regression-deploy-model.md)中，你将了解如何将模型存储到 SQL Server，然后从你在第二和第三部分中开发的 Python 脚本中创建存储过程。 存储过程将在 SQL Server 中运行，以便基于新数据进行预测。

## <a name="prerequisites"></a>先决条件

* 本教程的第二部分假设你已完成[第一个部分](python-ski-rental-linear-regression.md)及其必备组件。

## <a name="explore-and-prepare-the-data"></a>浏览和准备数据

若要在 Python 中使用数据，需将 SQL Server 数据库中的数据加载到 pandas 数据帧中。

在 Azure Data Studio 中创建新的 Python 笔记本，然后运行以下脚本。 将`<SQL Server>`替换为你自己的 SQL Server 名称。

下面的 Python 脚本将数据库中的**rental_data**表中的数据集导入到 pandas 数据帧**df**。

```python
import pandas as pd
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_import

# Connection string to your SQL Server instance
conn_str = 'Driver=SQL Server;Server=<SQL Server>;Database=TutorialDB;Trusted_Connection=True;'

# Define the columns you will import
 column_info = {
         "Year" : { "type" : "integer" },
         "Month" : { "type" : "integer" },
         "Day" : { "type" : "integer" },
         "RentalCount" : { "type" : "integer" },
         "WeekDay" : {
             "type" : "factor",
             "levels" : ["1", "2", "3", "4", "5", "6", "7"]
         },
         "Holiday" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         },
         "Snow" : {
             "type" : "factor",
             "levels" : ["1", "0"]
         }
     }

# Get the data from the SQL Server table
data_source = RxSqlServerData(table="dbo.rental_data",
                               connection_string=conn_str, column_info=column_info)
computeContext = RxInSqlServer(
     connection_string = conn_str,
     num_tasks = 1,
     auto_cleanup = False
)

RxInSqlServer(connection_string=conn_str, num_tasks=1, auto_cleanup=False)

# import data source and convert to pandas dataframe
df = pd.DataFrame(rx_import(input_data = data_source))
print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

应会看到如下所示的结果。

```results
Rows Processed: 453
Data frame:      Day  Holiday  Month  RentalCount  Snow  WeekDay  Year
0     20        1      1          445     2        2  2014
1     13        2      2           40     2        5  2014
2     10        2      3          456     2        1  2013
3     31        2      3           38     2        2  2014
4     24        2      4           23     2        5  2014
5     11        2      2           42     2        4  2015
6     28        2      4          310     2        1  2013
...
[453 rows x 7 columns]
```

## <a name="next-steps"></a>后续步骤

在本系列教程的第二部分中，您完成了以下步骤：

* 将 SQL Server 数据库中的数据加载到**pandas**数据帧中
* 通过删除某些列在 Python 中准备数据

若要训练使用 TutorialDB 数据库中的数据的机器学习模型，请遵循本教程系列中的第三部分：

> [!div class="nextstepaction"]
> [Python 教程：为线性回归模型定型](python-ski-rental-linear-regression-train-model.md)