---
title: 使用 Python 和 SQL 数据类型和对象
titleSuffix: SQL Server Machine Learning Services
description: 本快速入门介绍如何在 Python 中使用数据类型和数据对象，以及如何在 SQL Server 机器学习服务中 SQL Server。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 06540305d84ea16b76363ebb21cea0a246fd9ed8
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006056"
---
# <a name="quickstart-handle-data-types-and-objects-using-python-in-sql-server-machine-learning-services"></a>快速入门：在 SQL Server 中使用 Python 处理数据类型和对象机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入门演示了在 SQL Server 机器学习服务中使用 Python 时如何使用数据结构。

SQL Server 依赖于 Python **pandas**包，后者非常适合使用表格数据。 但是，不能将标量从 Python 传递到 SQL Server，并希望其 "只工作"。 在本快速入门中，你将了解一些基本数据类型定义，以便为你准备在 Python 和 SQL Server 之间传递表格数据时可能会遇到的其他问题。

前面需要了解的概念包括：

- 数据帧是包含_多个_列的表。
- 数据帧的单个列是一个类似列表的对象，称为 "序列"。
- 数据帧的单个值称为 "单元"，并由 "索引" 访问。

如果数据帧需要表格结构，如何将计算的单个结果公开为数据帧？ 一种答案是将单个标量值表示为序列，这可以轻松地转换为数据帧。 

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装了 Python 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 的实例。

- 还需要一个用于运行包含 Python 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="scalar-value-as-a-series"></a>作为序列的标量值

此示例执行一些简单的数学运算，并将标量转换为一个序列。

1. 序列需要索引，可以手动分配，如此处所示，或以编程方式分配。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   print(c)
   s = pandas.Series(c, index =["simple math example 1"])
   print(s)
   '
   ```

   由于该系列尚未转换为数据。帧，因此在 "消息" 窗口中返回值，但您可以看到这些结果的表格格式更多。

   **结果**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. 若要增加序列的长度，可以使用数组添加新的值。 

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   '
   ```

   如果不指定索引，则会生成一个索引，该索引的值从0开始，并以数组的长度结尾。

   **结果**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. 如果增加**索引**值的数目，但不添加新的**数据**值，则会重复数据值来填充序列。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   '
   ```

   **结果**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   simple math example 2    0.5
   dtype: float64
   ```

## <a name="convert-series-to-data-frame"></a>将序列转换为数据帧

将标量数学结果转换为表格结构后，仍需将它们转换为 SQL Server 可以处理的格式。

1. 若要将序列转换为数据框架，请调用 pandas[数据帧](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s)
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   结果如下所示。 即使使用索引从数据中获取特定值，索引值也不是输出的一部分。

   **结果**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>将值输出到数据帧中

现在，您将从两个数学序列结果中输出特定值。 第一个具有 Python 生成的顺序值的索引。 第二个使用字符串值的任意索引。

1. 下面的示例使用整数索引从序列获取值。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   d = a*b
   s = pandas.Series([c,d])
   print(s)
   df = pd.DataFrame(s, index=[1])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **结果**

   |ResultValue|
   |------|
   |2.0|

   请记住，自动生成的索引从0开始。 尝试使用超出范围的索引值并查看发生的情况。

1. 现在，使用字符串索引从另一个数据帧获取单个值。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   a = 1
   b = 2
   c = a/b
   s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
   print(s)
   df = pd.DataFrame(s, index=["simple math example 1"])
   OutputDataSet = df
   '
   WITH RESULT SETS((ResultValue FLOAT))
   ```

   **结果**

   |ResultValue|
   |------|
   |0.5|

   如果尝试使用数字索引获取此序列中的值，则会出现错误。

## <a name="next-steps"></a>后续步骤

若要了解如何在 SQL Server 中编写高级 Python 函数，请遵循以下快速入门：

> [!div class="nextstepaction"]
> [通过 SQL Server 机器学习服务写入高级 Python 函数](quickstart-python-functions.md)

有关在 SQL Server 机器学习服务中使用 Python 的详细信息，请参阅以下文章：

- [在 Python 中创建和评分预测模型](quickstart-python-train-score-model.md)
- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
