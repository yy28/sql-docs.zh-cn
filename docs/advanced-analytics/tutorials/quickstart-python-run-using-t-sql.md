---
title: 快速入门:"Hello World"基本 Python 代码执行 T-SQL 的 SQL Server 机器学习中
description: SQL Server 中的 Python 脚本的快速入门。 了解调用 Python 脚本在你好 world 练习使用 sp_execute_external_script 系统存储过程的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/11/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fb05e3b04fe9d6f33389e249d189baa7cc093016
ms.sourcegitcommit: 032273bfbc240fe22ac6c1f6601a14a6d99573f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2019
ms.locfileid: "55513767"
---
# <a name="quickstart-hello-world-python-script-in-sql-server"></a>快速入门：SQL Server 中的"hello world"Python 脚本 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入门教程，了解关键概念，通过运行"Hello World"Python 脚本 inT SQL，简介**sp_execute_external_script**系统存储过程。 

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 Python](quickstart-python-verify.md)、 提供的信息和链接设置为本快速入门所需的 Python 环境。

## <a name="basic-python-interaction"></a>Python 的基本交互

有两种方法在 SQL Server 中运行 Python 代码：

+ 系统存储过程的参数添加的 Python 脚本[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。

+ 从[远程 Python 客户端](../python/setup-python-client-tools-sql.md)，连接到 SQL Server，并使用 SQL Server 作为计算上下文执行代码。 这需要[revoscalepy](../python/ref-py-revoscalepy.md)。

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
+ 代码必须遵从所有关于缩进、 变量名称等的 Python 规则。 时遇到错误，检查您的空白区域和大小写。
+ 在编程语言之间 Python 是最灵活的一个方面单引号和双引号引起来;它们几乎可以互换。 但是，T-SQL 用于仅某些操作，单引号和`@script`参数使用单引号括起来的 Python 代码作为 Unicode 字符串。 因此，您可能需要查看您的 Python 代码，并将一些单引号更改为双引号引起来。
+ 如果使用的默认情况下不加载任何库，必须在脚本开头使用导入语句加载它们。 SQL Server 将添加几个特定于产品的库。 有关详细信息，请参阅[Python 库](../python/python-libraries-and-data-types.md)。
+ 如果库尚未安装，停止并安装 SQL Server 外部 Python 包，如下所述：[在 SQL Server 上安装新 Python 包](../python/install-additional-python-packages-on-sql-server.md)

## <a name="run-a-hello-world-script"></a>运行 Hello World 脚本

以下练习中运行另一个简单的 Python 脚本。

```sql
EXEC sp_execute_external_script
@language =N'Python',
@script=N'OutputDataSet = InputDataSet',
@input_data_1 =N'SELECT 1 AS hello'
WITH RESULT SETS (([Hello World] int));
GO
```

此存储过程的输入包括：

+ *@language* 参数定义的语言扩展。 若要调用，在这种情况下，Python。
+ *@script* 参数定义传递给 Python 运行时的命令。 为 Unicode 文本，整个 Python 脚本必须括在此参数。 还可将文本添加到 **nvarchar** 类型的变量并调用该变量。
+ *@input_data_1* 该查询中，传递给 Python 运行时，将数据返回到 SQL Server 作为数据帧返回数据。
+ 使用结果集子句返回的数据的表的架构定义的 SQL Server，将"Hello World"添加列名称，为**int**的数据类型。

**结果**

| 世界您好 |
|-------------|
| 1 |

## <a name="next-steps"></a>后续步骤

现在，已运行两个简单的 Python 脚本，需要深入研究构建输入和输出。

> [!div class="nextstepaction"]
> [快速入门：处理输入和输出](quickstart-python-inputs-and-outputs.md)
