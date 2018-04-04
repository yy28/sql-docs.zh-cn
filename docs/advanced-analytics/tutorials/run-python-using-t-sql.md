---
title: 运行 Python 使用 T-SQL |Microsoft 文档
ms.custom: ''
ms.date: 02/28/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
applies_to:
- SQL Server 2017
dev_langs:
- Python
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.openlocfilehash: cc14711d462ec53a7d40c025e30b5df4e60b2a9f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="run-python-using-t-sql"></a>运行 Python 使用 T-SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本教程介绍如何在 SQL Server 自 2017 年中运行 Python 代码。 它将指导你完成 SQL Server 和 Python 之间移动数据的过程，并解释了如何将格式正确的 Python 代码包装在存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)生成，训练，并使用在 SQL 中的机器学习模型服务器。

## <a name="prerequisites"></a>必要條件

若要完成本教程，必须先安装 SQL Server 2017 和中所述的实例上，启用机器学习服务[安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](../install/sql-machine-learning-services-windows-install.md)。 

你还应安装[SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)。 或者，你可以使用另一个数据库管理或查询工具，只要它可以连接到服务器和数据库，并且运行 T-SQL 查询或存储的过程。

完成安装程序后，返回到本教程中，若要了解如何在存储过程的上下文中执行 Python 代码。 

## <a name="overview"></a>概述

本教程包括以下四个课时：

+ SQL Server 和 Python 之间移动数据的基础知识： 了解基本要求、 数据结构、 输入和输出。
+ 使用简单的 Python 任务，例如，加载示例数据的存储的过程的做法。
+ 使用存储的过程来创建 Python 机器学习模型，并从该模型生成评分。
+ 要从远程客户端，使用 SQL Server 作为运行 Python 用户可选课_计算上下文_。 包含用于生成模型的代码但是，需要您已使用 Python 环境和 Python tools 比较熟悉。

此处提供的其他 Python 示例特定于 SQL Server 2017: [SQL Server Python 教程](../tutorials/sql-server-python-tutorials.md)

## <a name="verify-that-python-is-enabled-and-the-launchpad-is-running"></a>验证 Python 处于启用状态，运行快速启动板

1. 在 Management Studio 中运行本声明，以确保启用了服务。

    ```sql
    sp_configure 'external scripts enabled'
    ```

    如果**run_value**为 1，机器学习功能是已安装好可供使用。

    错误的常见原因是快速启动板，管理 SQL 服务器和 Python 之间的通信，已停止。 你可以通过使用 Windows 中查看的快速启动板状态**服务**面板，或通过打开 SQL Server 配置管理器。 如果服务已停止，重新启动它。

2. 接下来，验证 Python 运行时是使用且与 SQL Server 进行通信。 若要执行此操作，打开一个新**查询**窗口在 SQL Server Management Studio，并连接到 Python 已安装的实例。

    ```sql
    EXEC sp_execute_external_script @language = N'Python', 
    @script = N'print(3+4)'
    ```

    如果一切正常，你应看到如下所示的结果消息

    ```text
    STDOUT message(s) from external script: 
    7
    ```

3. 如果出现错误时，有许多你可以执行以确保服务器和 Python 可以进行通信的操作。 

    你必须添加 Windows 用户组`SQLRUserGroup`作为在实例中，以确保快速启动板可以提供 Python 和 SQL Server 之间的通信的登录名。 （同一组用于这两个 R 和 Python 代码执行。）有关详细信息，请参阅[默示身份验证的已启用](../r/add-sqlrusergroup-to-database.md)。
    
    此外，你可能需要启用已禁用的网络协议，或打开防火墙，以使 SQL Server 可以与外部客户端通信。 有关详细信息，请参阅[安装程序疑难解答](../common-issues-external-script-execution.md)。

## <a name="basic-python-interaction"></a>基本 Python 交互

有两种方法可以在 SQL Server 中运行 Python 代码：

+ 作为自变量的系统存储过程中，添加的 Python 脚本**sp_execute_external_script**
+ 从远程 Python 客户端，连接到 SQL Server 和执行使用 SQL Server 作为计算上下文的代码。 这要求[revoscalepy](../python/what-is-revoscalepy.md)。

本教程的主要目的是确保你可以在存储过程中使用 Python。

1. 运行一些简单的代码，若要查看如何数据 SQL 服务器和 Python 之间来回传递。

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

2. 假设您将拥有一切设置正确无误，并且彼此通信 Python 和 SQL Server，计算正确的结果，和 Python`print`函数返回将结果发送到**消息**windows。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```
    
    获取时**stdout**消息方便测试你的代码时，更频繁你需要执行以表格格式返回结果，以便可以在应用程序中使用它，也可以向表中写入。 

现在，请记住下列规则：

+ 内的所有内容`@script`参数必须是有效的 Python 代码。 
+ 代码必须遵循关于缩进、 变量名称和等的所有 Pythonic 规则。 时遇到错误，请检查你的空白区域和大小写。
+ 如果你使用的默认情况下不会加载任何库，必须在你的脚本的开头使用的导入语句加载它们。 
+ 如果库尚未安装，停止，并安装 SQL Server 外部的 Python 包，如下所述：[在 SQL Server 上安装新的 Python 软件包](../python/install-additional-python-packages-on-sql-server.md)

## <a name="inputs-and-outputs"></a>“脚本转换编辑器”

默认情况下， [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)接受单个输入数据集，通常你提供有效的 SQL 查询的表单中。 可以作为 SQL 变量传递其他类型的输入： 例如，你可以传递训练的模型作为变量，如使用序列化函数[pickle](https://docs.python.org/3.0/library/pickle.html)或[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)中编写模型二进制格式。

存储的过程返回的单个 Python [pandas](http://pandas.pydata.org/pandas-docs/stable/index.html)作为输出数据帧。 但是你可以作为变量输出标量和模型。 例如，您可以输出作为二进制变量训练的模型，以及传递给 T-SQL INSERT 语句，以向表中写入该模型。 你还可以生成图形 （采用二进制格式） 或标量 （单个值，如日期和时间，经过的时间来训练该模型，等等）。

现在，让我们看一下默认值只是输入和输出变量`InputDataSet`和`OutputDataSet`。 

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

2. 你应收到错误，因为 Python 代码生成标量，不数据帧。

        **Results**

        ```text
        line 43, in transform
            raise TypeError('OutputDataSet should be of type pandas.DataFrame')
        ```

3. 现在请参阅使用默认输入的变量向 Python，传递的表格数据集时，会发生什么情况`InputDataSet`。 

    ```sql
    EXECUTE sp_execute_external_script 
    @language = N'Python', 
    @script = N'
    OutputDataSet = InputDataSet
    ',
    @input_data_1 = N'SELECT 1 as Col1'
    ```

    存储的过程返回 data.frame 自动，您无需进行任何额外 Python 代码中。

    **结果**

    | 没有列名称|
    |------|
    | 1|

    默认情况下，单个表格输入数据集具有该名称， `InputDataSet`。 但是，可以通过添加类似的行更改该名称： `@input_data_1_name = N'myResultName'`。

    使用 Python 的列名称永远不会保留在输出中。 尽管输入的查询指定的列名称但`Col1`、 未返回该名称，也不会使用你的 Python 脚本的任何列标题。 若要将数据返回到 SQL Server 时，请指定列名称和数据类型，使用 T-SQL 的`WITH RESULT SETS`子句。

4. 此示例中提供的输入和输出的变量的新名称。

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

    与结果集子句定义的输出架构，因为 Python 列名称将永远不会返回 data.frame。

    **结果**

    | ResultValue|
    |------|
    | 1|

5. 现在让我们看一下典型的 Python 错误。 更改从上一示例中的行`@input_data_1_name = N'MyInput'`到`@input_data_1_name = N'myinput'`。

    Python 错误通过使用 SQL Server 的附属服务传递给你作为消息。 消息可以比较长，而且包括 SQL Server 错误或快速启动板错误以及 Python 错误，因此请深入整个文本中的耐心等待。 关键信息是在此行中：

    ```text
    MyOutput = MyInput
    NameError: name 'MyInput' is not defined
    ```

    回想一下，Python，如 R，是区分大小写。 因此，当您获取任何类型的错误，请确保检查变量的名称，并查找间距、 缩进，与数据类型的问题。

## <a name="python-data-structures"></a>Python 数据结构

SQL Server 依赖于 Python **pandas**包，其中非常适合使用表格数据。 但是，你已经了解不能将一个标量从 Python 传递到 SQL Server 和期待它"正常工作"。 在此部分中，我们将查看一些基本数据类型定义，以你为在 Python 和 SQL Server 之间传递表格数据时可能遇到的更多问题做好准备。

+ 数据帧是一个表，其中_多个_列。
+ 包含一列的数据帧，是调用一系列的列表类似对象。
+ 单个值的数据框架的单元格而必须由索引。

那么，如何将你公开单个计算的结果的作为数据框架，如果 data.frame 需要表格结构？ 一个答案是作为一系列，轻松地转换为数据帧表示单个标量值。 

1. 此示例未一些简单的数学，并将一个标量转换成一系列。 一系列需要如下所示，手动或以编程方式可以分配的索引。

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

2. 因为序列尚未转换为 data.frame 后，将值返回在消息窗口中，但你可以看到的结果更表格格式。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5
    simple math example 1    0.5
    dtype: float64
    ```

3. 若要增加序列的长度，可以添加新值，使用数组。 

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

    如果未指定索引，索引会生成具有值从 0 开始和结束与数组的长度。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0    0.5
    1    2.0
    dtype: float64
    ```

4. 如果增加的数量**索引**值，但不添加新**数据**值，数据值重复以填充序列。

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

### <a name="convert-series-to-data-frame"></a>将序列转换为数据帧

无转换为表格结构我们标量数学函数的结果，我们仍需要将它们转换为 SQL Server 可以处理的格式。 

1. 若要将一系列转换为 data.frame，调用 pandas[数据帧](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dataframe)方法。

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

2. 请注意索引值不是输出，即使你使用索引从 data.frame 获取特定值。

    **结果**

    |ResultValue|
    |------|
    |0.5|
    |2|

### <a name="output-values-into-dataframe-using-an-index"></a>输出值插入 data.frame 使用索引

让我们了解我们包含简单的数学运算结果的两个序列时，转换为 data.frame 的工作原理。 第一个已生成的 Python 的顺序值的索引。 第二个使用任意字符串值的索引。

1. 此示例使用整数索引序列中获取一个值。

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

    请记住从 0 开始的自动生成的索引。 尝试使用范围索引值外，请参阅会发生什么情况。

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

    如果你尝试使用数字索引这一系列从获取一个值，则会出现错误。

本练习旨在让你了解如何使用不同的 Python 数据结构，并确保你获得正确的结果作为数据框架。 你可能已得出结论的数据帧原样代价高于其相当于该输出单个值 ！ 幸运的是，可以轻松地将所有类型的值和存储过程退出都传递作为变量。 下一课中介绍了的。

## <a name="tips"></a>提示

+ 在编程语言中，Python 是最灵活之一方面单引号和双引号引起来;这些更改将几乎可互换。 

    但是，T-SQL 用于仅的某些事项，单引号和`@script`参数使用单引号括起为 Unicode 字符串的 Python 代码。 因此，你可能需要查看你的 Python 代码，并将一些单引号更改为双引号引起来。

+ 找不到存储的过程， `sp_execute_external_script`？ 这意味着你可能尚未完成的配置要支持外部脚本执行的实例。 运行 SQL Server 2017 安装程序并选择后 Python 作为机器学习语言，则必须还在显式启用功能使用`sp_configure`，然后重新启动实例。 

    有关详细信息，请参阅[安装 SQL Server 自 2017 年 1 机器学习 Services （数据库）](../install/sql-machine-learning-services-windows-install.md)。

## <a name="next-steps"></a>后续步骤

[将 Python 代码包装在一个 SQL 存储过程](wrap-python-in-tsql-stored-procedure.md)