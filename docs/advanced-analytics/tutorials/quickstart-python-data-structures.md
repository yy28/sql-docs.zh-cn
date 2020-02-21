---
title: 快速入门：Python 数据结构
description: 在本快速入门中，了解如何在 SQL Server 机器学习服务中使用 Python 处理数据结构和数据对象。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 0f04e021664a92241c8c029d296a298b10c142d2
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "76831904"
---
# <a name="quickstart-data-structures-and-objects-using-python-in-sql-server-machine-learning-services"></a>快速入门：在 SQL Server 机器学习服务中使用 Python 处理数据结构和对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入门介绍在 SQL Server 机器学习服务中使用 Python 时如何使用数据结构。

SQL Server 依赖于 Python 的 pandas 包，该包非常适合处理表格数据  。 但是，不能将标量从 Python 传递到 SQL Server 并期望它“正常运行”。 在本快速入门中，你将回顾一些基本的数据结构定义，以便为在 Python 和 SQL Server 之间传递表格数据时可能遇到的其他问题做好准备。

需预先了解的概念包括：

- 数据帧是包含多列  的表。
- 数据帧的单列是一个类似于列表的对象，称为“序列”。
- 数据帧的单个值称为单元格，并由索引访问。

如果数据帧需要表格结构，那么如何将计算的单个结果公开为数据帧？ 一种答案是将单个标量值表示为一个序列，该序列很容易转换为数据帧。 

> [!NOTE]
> 返回日期时，SQL 中的 Python 使用 DATETIME，其受限制的日期范围是 1753-01-01(-53690) 到 9999-12-31(2958463)。 

## <a name="prerequisites"></a>必备条件

- 本快速入门需要使用安装了 Python 语言的 [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 实例。

- 你还需要一个工具来运行包含 Python 脚本的 SQL 查询。 可使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，并运行 T-SQL 查询或存储过程即可。 本快速入门使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="scalar-value-as-a-series"></a>作为序列的标量值

此示例执行一些简单的数学运算，并将标量转换成序列。

1. 序列需要索引，可以手动分配，如图所示，或以编程方式分配。

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

   由于序列尚未转换为数据帧，因此将在“消息”窗口中返回值，但你可以看到结果的格式更为表格化。

   **结果**

   ```text
   STDOUT message(s) from external script: 
   0.5
   simple math example 1    0.5
   dtype: float64
   ```

1. 要增加序列的长度，可以使用数组添加新值。 

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

   如果未指定索引，则会生成一个索引，其值以 0 开头，以数组长度结尾。

   **结果**

   ```text
   STDOUT message(s) from external script: 
   0    0.5
   1    2.0
   dtype: float64
   ```

1. 如果增加索引值的数目，但不添加新的数据值，则将重复使用数据值来填充序列   。

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

将标量数学结果转换为表格结构后，仍需将其转换为 SQL Server 可以处理的格式。

1. 若要将序列转换为数据帧，请调用 pandas [数据帧](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

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

   结果如下所示。 即使使用索引从数据帧中获取特定值，索引值也不是输出的一部分。

   **结果**

   |ResultValue|
   |------|
   |0.5|
   |2|

## <a name="output-values-into-dataframe"></a>将值输出到数据帧中

现在，你将在数据帧中输出两个数学结果序列中的特定值。 第一个是由 Python 生成的序列值索引。 第二个使用字符串值的任意索引。

1. 以下示例使用整数索引从序列中获取值。

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

   请记住，自动生成的索引从 0 开始。 尝试使用超出范围的索引值并查看发生的情况。

1. 现在使用字符串索引从另一个数据帧中获取单个值。

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

   如果试图使用数字索引从该序列中获取值，则会出现错误。

## <a name="next-steps"></a>后续步骤

若要了解如何在 SQL Server 中编写高级 Python 函数，请遵循以下快速入门：

> [!div class="nextstepaction"]
> [使用 SQL Server 机器学习服务编写高级 Python 函数](quickstart-python-functions.md)

有关在 SQL Server 机器学习服务中使用 Python 的详细信息，请参阅以下文章：

- [在 Python 中创建预测模型并对其进行评分](quickstart-python-train-score-model.md)
- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
