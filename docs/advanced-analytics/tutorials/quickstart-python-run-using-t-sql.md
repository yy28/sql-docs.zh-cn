---
title: 用于 T-sql 中的 "Hello World" 基本 Python 代码执行的快速入门
description: SQL Server 中的 Python 脚本快速入门。 了解使用 sp_execute_external_script 系统存储过程在系统中调用 Python 脚本的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/10/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1281da6a366f7fa9d5fca20cc719a3c86825e56d
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469618"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>快速入门：SQL Server 中的 "Hello world" Python 脚本 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中, 通过运行 "Hello World" Python script inT-SQL 了解关键概念, 并介绍**sp_execute_external_script**系统存储过程。 

## <a name="prerequisites"></a>先决条件

之前的快速入门,[请验证 SQL Server 中是否存在 python](quickstart-python-verify.md), 并提供设置此快速入门所需的 Python 环境所需的信息和链接。

## <a name="basic-python-interaction"></a>基本 Python 交互

可以通过两种方式在 SQL Server 中运行 Python 代码:

+ 添加 Python 脚本作为系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)的参数。

+ 从[远程 Python 客户端](../python/setup-python-client-tools-sql.md), 连接到 SQL Server, 并使用 SQL Server 作为计算上下文来执行代码。 这需要[revoscalepy](../python/ref-py-revoscalepy.md)。

以下练习重点介绍第一种交互模型: 如何将 Python 代码传递到存储过程。

1. 运行一些简单的代码, 以了解如何在 SQL Server 和 Python 之间来回传递数据。

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

2. 假设你已正确设置了所有内容, 并且 python 和 SQL Server 互相通信, 则会计算正确的结果, Python `print`函数会将结果返回给**消息**窗口。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    虽然在测试代码时获取**stdout**消息很方便, 但更多情况下, 需要以表格格式返回结果, 以便在应用程序中使用它或将其写入表。

现在, 请记住以下规则:

+ 参数内的`@script`所有内容都必须是有效的 Python 代码。 
+ 代码必须遵循有关缩进、变量名称等的所有 Python 规则。 出现错误时, 请检查您的空白和大小写。
+ 在编程语言中, Python 是最灵活的单引号与双引号之间的比较;它们非常可互换。 但是, t-sql 仅对某些东西使用单引号, 而`@script`参数使用单引号将 Python 代码作为 Unicode 字符串。 因此, 你可能需要查看 Python 代码, 并将一些单引号更改为双引号。
+ 如果你使用的是默认情况下未加载的任何库, 则必须在脚本开头使用 import 语句来加载这些库。 SQL Server 添加几个特定于产品的库。 有关详细信息, 请参阅[Python 库](../python/python-libraries-and-data-types.md)。
+ 如果尚未安装库, 请在 SQL Server 之外停止并安装 Python 包, 如下所述:[在 SQL Server 上安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>运行 Hello World 脚本

以下练习将运行另一个简单的 Python 脚本。

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

此存储过程的输入包括:

+ *@language* 参数定义要调用的语言扩展, 在本例中为 Python。
+ *@script* 参数定义传递到 Python 运行时的命令。 整个 Python 脚本必须以 Unicode 文本的形式包含在此参数中。 还可将文本添加到 **nvarchar** 类型的变量并调用该变量。
+ *@input_data_1* 查询返回的数据, 传递到 Python 运行时, 它将数据作为数据帧返回 SQL Server。
+ WITH RESULT SETS 子句为 SQL Server 定义返回的数据表的架构, 并将 "Hello World" 添加为列名称, 为数据类型输入**int** 。

**结果**

| 世界您好 |
|-------------|
| 1 |

## <a name="next-steps"></a>后续步骤

现在, 你已运行了几个简单的 Python 脚本, 接下来详细介绍了如何构建输入和输出。

> [!div class="nextstepaction"]
> [起步处理输入和输出](quickstart-python-inputs-and-outputs.md)
