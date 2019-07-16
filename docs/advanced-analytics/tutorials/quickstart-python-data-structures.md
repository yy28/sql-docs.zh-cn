---
title: 快速入门： 使用 Python-SQL Server 机器学习中的数据结构
description: 在本快速入门中的 Python 脚本在 SQL Server 中，了解如何使用数据结构使用 sp_execute_external_script 的系统存储过程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: ffbbd39c08221db4afa6427626ca618e04617166
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962081"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>快速入门：SQL Server 中的 Python 数据结构
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本快速入门介绍如何在 SQL Server 机器学习服务中使用 Python 时使用的数据结构。

SQL Server 依赖于 Python **pandas**包，这非常适用于使用表格数据。 但是，不能将标量 Python 从传递到 SQL Server，并且希望它"正常工作"。 在本快速入门，我们将回顾一些基本数据类型定义，以你为 Python 和 SQL Server 之间传递的表格数据时可能遇到的其他问题做好准备。

+ 数据帧是包含的表_多个_列。
+ 包含一列的数据帧，是调用一系列类似于列表的对象。
+ 单个值是一个单元格的数据帧，并已调用的索引。

您如何将公开单个计算结果的作为数据帧时，如果 data.frame 需要表格结构？ 一个答案是为一系列，轻松地转换为数据帧中表示单个标量值。 

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 Python](quickstart-python-verify.md)、 提供的信息和链接设置为本快速入门所需的 Python 环境。

## <a name="scalar-value-as-a-series"></a>为一系列的标量值

此示例 does 一些简单的数学运算并转换为一系列的标量。

1. 一系列需要索引，可以如下所示，手动或以编程方式分配。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    s = pandas.Series(c, index =["simple math example 1"])
    print(s)
    '
    ```

2. 由于尚未被序列转换为 data.frame，在消息窗口中，返回的值，但可以看到结果是一个更表格中。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. 若要增加序列的长度，可以添加新值，使用一个数组。 

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    s = pandas.Series([c,d])
    print(s)
    '
    ```

    如果未指定索引，索引生成具有值从 0 开始和结尾的数组的长度。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. 如果增加的数量**索引**值，但不添加新**数据**值，重复数据值填充序列。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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

## <a name="convert-series-to-data-frame"></a>将序列转换成数据帧

让我们标量数学函数的结果转换为表格结构时，我们仍需要将它们转换为 SQL Server 可以处理的格式。 

1. 若要将序列转换为 data.frame，调用 pandas[数据帧](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

2. 结果如下所示。 即使使用索引来从 data.frame 中获取特定值，索引值不是输出的一部分。

    **结果**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>到 data.frame 的输出值

让我们了解我们包含结果的简单数学运算的两个序列时，转换为 data.frame 的工作原理。 第一个具有由 Python 生成的顺序值的索引。 第二个使用任意字符串值的索引。

1. 此示例中使用整数索引序列中获取一个值。

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
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
    WITH RESULT SETS (( ResultValue float ))
    ```

    请记住，自动生成索引从 0 开始。 尝试使用范围索引值，看会发生什么情况。

2. 现在让我们从其他具有字符串索引的数据帧中获取单个值。 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    import pandas as pd
    a = 1
    b = 2
    c = a/b
    s = pandas.Series(c, index =["simple math example 1", "simple math example 2"])
    print(s)
    df = pd.DataFrame(s, index=["simple math example 1"])
    OutputDataSet = df
    '
    WITH RESULT SETS (( ResultValue float ))
    ```

    **结果**

    |ResultValue|
    |------|
    |0.5|

    如果你尝试使用数字索引获取此序列中的值，可能会出错。

## <a name="next-steps"></a>后续步骤

接下来，你将构建一个在 SQL Server 中使用 Python 的预测模型。

> [!div class="nextstepaction"]
> [创建、 定型和 SQL Server 中使用存储过程中使用 Python 模型](quickstart-python-train-score-in-tsql.md)