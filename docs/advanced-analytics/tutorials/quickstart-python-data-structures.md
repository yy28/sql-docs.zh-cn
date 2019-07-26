---
title: 使用 Python 中的数据结构的快速入门
description: 在 SQL Server 中的 Python 脚本的此快速入门教程中, 了解如何将数据结构与 sp_execute_external_script 系统存储过程一起使用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 17b2c150368b32960907d6fdd2e31b109f51d771
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469640"
---
# <a name="quickstart-python-data-structures-in-sql-server"></a>快速入门：SQL Server 中的 Python 数据结构
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入门演示了在 SQL Server 机器学习服务中使用 Python 时如何使用数据结构。

SQL Server 依赖于 Python **pandas**包, 后者非常适合使用表格数据。 但是, 不能将标量从 Python 传递到 SQL Server, 并希望其 "只工作"。 在本快速入门中, 我们将查看一些基本的数据类型定义, 以便为你准备在 Python 和 SQL Server 之间传递表格数据时可能会遇到的其他问题。

+ 数据帧是包含_多个_列的表。
+ 数据帧的单个列是一个类似列表的对象, 称为 "序列"。
+ 单个值是数据帧的单元格, 必须由 index 调用。

如果数据帧需要表格结构, 如何将计算的单个结果公开为数据帧？ 一种答案是将单个标量值表示为序列, 这可以轻松地转换为数据帧。 

## <a name="prerequisites"></a>先决条件

之前的快速入门,[请验证 SQL Server 中是否存在 python](quickstart-python-verify.md), 并提供设置此快速入门所需的 Python 环境所需的信息和链接。

## <a name="scalar-value-as-a-series"></a>作为序列的标量值

此示例执行一些简单的数学运算, 并将标量转换为一个序列。

1. 序列需要索引, 可以手动分配, 如此处所示, 或以编程方式分配。

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

2. 由于该系列尚未转换为数据。帧, 因此在 "消息" 窗口中返回值, 但您可以看到这些结果的表格格式更多。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. 若要增加序列的长度, 可以使用数组添加新的值。 

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

    如果不指定索引, 则会生成一个索引, 该索引的值从0开始, 并以数组的长度结尾。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. 如果增加**索引**值的数目, 但不添加新的**数据**值, 则会重复数据值来填充序列。

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

## <a name="convert-series-to-data-frame"></a>将序列转换为数据帧

将标量数学结果转换为表格结构后, 我们仍然需要将它们转换为 SQL Server 可以处理的格式。 

1. 若要将序列转换为数据框架, 请调用 pandas[数据帧](https://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

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

2. 结果如下所示。 即使使用索引从数据中获取特定值, 索引值也不是输出的一部分。

    **结果**

    |ResultValue|
    |------|
    |0.5|
    |2|

## <a name="output-values-into-dataframe"></a>将值输出到数据帧中

让我们看看如何转换为数据。 frame 适用于包含简单数学运算结果的两个系列。 第一个具有 Python 生成的顺序值的索引。 第二个使用字符串值的任意索引。

1. 此示例从使用整数索引的序列获取值。

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

    请记住, 自动生成的索引从0开始。 尝试使用超出范围的索引值并查看发生的情况。

2. 现在, 让我们从具有字符串索引的其他数据帧获取单个值。 

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

    如果尝试使用数字索引获取此序列中的值, 则会出现错误。

## <a name="next-steps"></a>后续步骤

接下来, 您将在 SQL Server 中使用 Python 构建预测模型。

> [!div class="nextstepaction"]
> [使用中的存储过程创建、定型和使用 Python 模型 SQL Server](quickstart-python-train-score-in-tsql.md)