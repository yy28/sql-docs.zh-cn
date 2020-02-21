---
title: Python 教程：准备数据
description: 本教程系列由四个部分组成，在第二部分中，你将在 SQL Server 机器学习服务中使用 Python 准备数据，以预测雪橇租赁次数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/02/2020
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9aeefb0b6fd9ca1a744d132fccf1eedfedbaa6e7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "75681741"
---
# <a name="python-tutorial-prepare-data-to-train-a-linear-regression-model-in-sql-server-machine-learning-services"></a>Python 教程：在 SQL Server 机器学习服务中准备数据以定型线性回归模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

此教程包括四分部分，在第二部分中，你将使用 Python 准备 SQL Server 数据库中的数据。 在本系列的后面部分，你将通过 SQL Server 机器学习服务在 Python 中使用此数据定型和部署线性回归模型。

本文将指导如何进行以下操作：

> [!div class="checklist"]
> * 将 SQL 数据库中的数据加载到 pandas 数据帧中 
> * 通过删除某些列，在 Python 中准备数据

在[第一部分](python-ski-rental-linear-regression.md)中，你了解了如何还原示例数据库。

[第三部分](python-ski-rental-linear-regression-train-model.md)中已介绍如何在 Python 中定型线性回归机器学习模型。

[第四部分](python-ski-rental-linear-regression-deploy-model.md)介绍如何将模型存储到 SQL Server，然后根据在第二和第三部分中开发的 Python 脚本来创建存储过程。 存储过程将在 SQL Server 中运行，以便基于新数据进行预测。

## <a name="prerequisites"></a>必备条件

* 本教程的第二部分假设你已完成[第一部分](python-ski-rental-linear-regression.md)且满足其必备条件。

## <a name="explore-and-prepare-the-data"></a>浏览和准备数据

若要在 Python 中使用数据，请将 SQL 数据库中的数据加载到 pandas 数据帧中。

在 Azure Data Studio 中创建新的笔记本，并运行以下脚本。 将 `<SQL Server>` 替换为自己的 SQL Server 名称。

下面的 Python 脚本将数据库中 dbo.rental_data 表中的数据集导入到 pandas 数据帧 df   。

在连接字符串中，根据需要替换连接详细信息。

```python
import pyodbc
import pandas
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error

# Connection string to your SQL Server instance
conn_str = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server}; SERVER=localhost; DATABASE=TutorialDB; Trusted_Connection=yes')

query_str = 'SELECT Year, Month, Day, Rentalcount, Weekday, Holiday, Snow FROM dbo.rental_data'

df = pandas.read_sql(sql=query_str, con=conn_str)

print("Data frame:", df)

# Get all the columns from the dataframe.
columns = df.columns.tolist()

# Filter the columns to remove ones we don't want to use in the training
columns = [c for c in columns if c not in ["Year"]]
```

可得到类似于下面的结果。

```results
Data frame:      Year  Month  Day  RentalCount  WeekDay  Holiday  Snow
0    2014      1   20          445        2        1     0
1    2014      2   13           40        5        0     0
2    2013      3   10          456        1        0     0
3    2014      3   31           38        2        0     0
4    2014      4   24           23        5        0     0
..    ...    ...  ...          ...      ...      ...   ...
448  2013      2   19           57        3        0     1
449  2015      3   18           26        4        0     0
450  2015      3   24           29        3        0     1
451  2014      3   26           50        4        0     1
452  2015     12    6          377        1        0     1

[453 rows x 7 columns]
```

## <a name="next-steps"></a>后续步骤

在本教程系列的第二部分中，你已完成这些步骤：

* 将 SQL 数据库中的数据加载到 pandas 数据帧中 
* 通过删除某些列，在 Python 中准备数据

若要对使用 TutorialDB 数据库中数据的机器学习模型进行定型，请按照本教程系列的第三部分进行操作：

> [!div class="nextstepaction"]
> [Python 教程：定型线性回归模型](python-ski-rental-linear-regression-train-model.md)