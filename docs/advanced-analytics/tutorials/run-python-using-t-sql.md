---
title: 运行 SQL Server 上使用 T-SQL 的 Python |Microsoft Docs
description: 了解运行 SQL Server 数据库引擎实例为其启用 Python 集成上使用 T-SQL 和存储的过程的 Python 代码的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e22b280c4fea395f8c7cf7c4b559d5ff5a22d6c1
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461913"
---
# <a name="run-python-using-t-sql"></a>使用 T-SQL 运行 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍如何在 SQL Server 2017 中运行 Python 代码。 它将指导你完成 SQL Server 和 Python 之间移动数据的基础知识： 要求、 数据结构、 输入和输出。 它还介绍了如何将格式正确的 Python 代码包装在存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)来生成、 训练和使用 SQL Server 中机器学习模型。

## <a name="prerequisites"></a>必要條件

若要运行示例代码在这些练习中，必须首先安装 SQL Server 2017 和机器学习服务实例上启用，如中所述[安装 SQL Server 2017 机器学习服务 （数据库内）](../install/sql-machine-learning-services-windows-install.md)。 

此外应安装[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。 或者，可以使用其他数据库管理或查询工具，前提是它可以连接到服务器和数据库，并运行 T-SQL 查询或存储的过程。

你的环境准备就绪后，返回到此页以了解如何在存储过程的上下文中执行 Python 代码。 

## <a name="verify-python-exists"></a>验证存在 Python

以下步骤确认已启用 Python 和 SQL Server 快速启动板服务正在运行。

1. 检查数据库引擎实例上是否安装了 Python 集成。 您会发现**python.exe**中名为的文件夹**PYTHON_SERVICES**在 C:\Program Files\Microsoft SQL Server\MSSQL14。MSSQLSERVER\. 这是 SQL Server 使用来运行 Python 代码的 Python 可执行文件。

2. 检查是否已启用外部脚本。 在 Management Studio 中运行以下语句：

    ```sql
    sp_configure 'external scripts enabled'
    ```

    如果**run_value**为 1，机器学习功能是已安装并可供使用。

    错误的常见原因是该[SQL Server Launchpad 服务](../concepts/extensibility-framework.md#launchpad)，用于管理 SQL Server 和 Python 之间的通信已停止。 您可以使用 Windows 查看快速启动板状态**Services**面板，或通过打开 SQL Server 配置管理器。 如果服务停止后，重新启动它。

3. 验证 Python 运行时工作，并与 SQL Server 通信。 若要执行此操作，打开一个新**查询**窗口在 SQL Server Management Studio 并连接到已安装 Python 的实例。

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    如果一切正常，应看到类似如下的结果消息

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. 如果收到错误，有很多可以执行以确保可以进行通信的服务器和 Python 的事情。 

    您必须添加 Windows 用户组`SQLRUserGroup`上的实例，以确保快速启动板可以提供 Python 和 SQL Server 之间的通信的登录名。 （同一个组用于这两个 R 和 Python 代码执行）。有关详细信息，请参阅[已启用隐式身份验证](../security/add-sqlrusergroup-to-database.md)。
    
    此外，您可能需要启用已禁用的网络协议或打开防火墙，以便 SQL Server 可以与外部客户端进行通信。 有关详细信息，请参阅[安装程序疑难解答](../common-issues-external-script-execution.md)。

## <a name="basic-python-interaction"></a>Python 的基本交互

有两种方法在 SQL Server 中运行 Python 代码：

+ 系统存储过程的参数添加的 Python 脚本[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 从[远程 Python 客户端](../python/setup-python-client-tools-sql.md)，连接到 SQL Server，并使用 SQL Server 作为计算上下文执行代码。 这需要[revoscalepy](../python/what-is-revoscalepy.md)。

以下练习的重点是第一个交互模型： 如何将 Python 代码传递给存储过程。

1. 运行一些简单代码，请参阅如何数据 SQL 服务器和 Python 之间来回传递。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

2. 假设你有所有内容设置正确无误，并且 Python 和 SQL Server 是否在与彼此通信，计算正确的结果，和 Python`print`函数将返回到结果**消息**windows。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    获取时**stdout**测试你的代码时，消息是非常方便，更频繁地需要以表格格式返回结果，以便可以在应用程序中使用它或将其写入到一个表。 

现在，请记住以下规则：

+ 内的所有内容`@script`参数必须是有效的 Python 代码。 
+ 代码必须遵循有关缩进、 变量名称等所有 Pythonic 规则。 时遇到错误，检查您的空白区域和大小写。
+ 如果使用的默认情况下不加载任何库，必须在脚本开头使用导入语句加载它们。 SQL Server 将添加几个特定于产品的库。 有关详细信息，请参阅[Python 库](../python/python-libraries-and-data-types.md)。
+ 如果库尚未安装，停止并安装 SQL Server 外部 Python 包，如下所述： [SQL Server 上安装新的 Python 包](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>“脚本转换编辑器”

默认情况下[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)接受单个输入数据集，这通常中有效的 SQL 查询的形式提供。 

可以作为 SQL 变量传递其他类型的输入： 例如，您可以传递训练的模型作为变量，如使用序列化函数[pickle](https://docs.python.org/3.0/library/pickle.html)或[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)中编写模型二进制格式。

存储的过程返回单个 Python [pandas](http://pandas.pydata.org/pandas-docs/stable/index.html)数据帧为 output，但您也可以输出标量和作为变量的模型。 例如，可以输出为二进制变量已训练的模型，并将其传递给 T-SQL INSERT 语句，该模型写入表。 您还可以生成绘图 （以二进制格式） 或标量 （单个值，如日期和时间，经过的时间来训练该模型，等等）。

现在，让我们看看只是默认的 sp_execute_external_script 的输入和输出变量：`InputDataSet`和`OutputDataSet`。 

1. 运行以下代码以执行某些数学运算，并输出结果。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    a = 1
    b = 2
    c = a/b
    print(c)
    OutputDataSet = c
    '
    WITH RESULT SETS ((ResultValue float))
    ```

2. 应显示错误，因为在 Python 代码中生成一个标量数据帧。

    **结果**

    ```text
    line 43, in transform
        raise TypeError('OutputDataSet should be of type pandas.DataFrame')
    ```

3. 现在，看到使用默认输入的变量向 Python，传递表格数据集时，会发生什么情况`InputDataSet`。 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    存储的过程返回 data.frame 自动，而无需执行任何额外操作在 Python 代码中。

    **结果**

    | 没有列名称|
    |------|
    | 1|

    默认情况下，单个表格输入数据集的名称， `InputDataSet`。 但是，可以通过添加类似的行来更改该名称： `@input_data_1_name = N'myResultName'`。

    通过 Python 使用列名称将永远不会保留在输出中。 虽然输入的查询指定列名称`Col1`、 不返回该名称，也不会使用 Python 脚本的任何列标题。 若要将数据返回到 SQL Server 时，请指定列名称和数据类型，使用 T-SQL 的`WITH RESULT SETS`子句。

4. 此示例提供了新的输入和输出变量名称。

    ```sql
    execute sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    MyOutput = MyInput
    ',
    @input_data_1_name = N'MyInput',
    @input_data_1 = N'SELECT 1 as Col1',
    @output_data_1_name = N'MyOutput'
    WITH RESULT SETS ((ResultValue int))
    ```

    使用结果集子句定义的输出架构由于 Python 列名称将永远不会返回数据帧。

    **结果**

    | ResultValue|
    |------|
    | 1|

5. 现在让我们看看典型的 Python 错误。 更改从前面的示例中的行`@input_data_1_name = N'MyInput'`到`@input_data_1_name = N'myinput'`。

    Python 错误参数传递给您作为消息，通过使用 SQL Server 的附属服务。 消息可以很长并包括 SQL Server 错误或快速启动板错误除了 Python 错误保持耐心获知文本中的。 要点是： 此行中：

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    请注意，Python、，是区分大小写。 因此时获取任何类型的错误，请, 务必检查您变量的名称，并查找的间距、 缩进和数据类型的问题。

## <a name="python-data-structures"></a>Python 数据结构

SQL Server 依赖于 Python **pandas**包，这非常适用于使用表格数据。 但是，您所见，不能将标量 Python 从传递到 SQL Server，并且希望它"正常工作"。 在本部分中，我们将回顾一些基本数据类型定义，以你为 Python 和 SQL Server 之间传递的表格数据时可能遇到的其他问题做好准备。

+ 数据帧是包含的表_多个_列。
+ 包含一列的数据帧，是调用一系列类似于列表的对象。
+ 单个值是一个单元格的数据帧，并已调用的索引。

那么，如何将您公开单个计算结果的作为数据帧时，如果 data.frame 需要表格结构？ 一个答案是为一系列，轻松地转换为数据帧中表示单个标量值。 

1. 此示例 does 一些简单的数学运算并转换为一系列的标量。 一系列需要索引，可以如下所示，手动或以编程方式分配。

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

### <a name="convert-series-to-data-frame"></a>将序列转换成数据帧

让我们标量数学函数的结果转换为表格结构时，我们仍需要将它们转换为 SQL Server 可以处理的格式。 

1. 若要将序列转换为 data.frame，调用 pandas[数据帧](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

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

2. 请注意索引值不是输出中，即使使用索引来从 data.frame 中获取特定的值。

    **结果**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>输出值到 data.frame 使用索引

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

本练习中原来是为了让您了解如何使用不同的 Python 数据结构，确保获得正确结果作为数据帧。 可能会结束该将输出单个值的数据帧原样代价高于其价值 ！ 幸运的是，可以轻松地将所有类型的传入和传出该存储过程的值都传递为变量。 下一课中介绍了的。

## <a name="tips"></a>提示

+ 在编程语言之间 Python 是最灵活的一个方面单引号和双引号引起来;它们几乎可以互换。 

    但是，T-SQL 用于仅某些操作，单引号和`@script`参数使用单引号括起来的 Python 代码作为 Unicode 字符串。 因此，您可能需要查看您的 Python 代码，并将一些单引号更改为双引号引起来。

+ 找不到该存储的过程， `sp_execute_external_script`？ 这意味着您可能没有完成配置要支持外部脚本执行的实例。 运行 SQL Server 2017 安装程序并选择 Python 作为机器学习语言之后, 您必须显式启用功能使用`sp_configure`，然后重新启动实例。 

    有关详细信息，请参阅[安装 SQL Server 2017 机器学习服务 （数据库内）](../install/sql-machine-learning-services-windows-install.md)。

## <a name="next-steps"></a>后续步骤

[设置鸢尾花演示数据集](demo-data-iris-in-sql.md)