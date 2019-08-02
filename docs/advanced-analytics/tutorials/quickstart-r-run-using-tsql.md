---
title: T-sql 中的 "Hello World" 基本 R 代码执行的快速入门
description: SQL Server 中的 R 脚本快速入门。 了解使用 sp_execute_external_script 系统存储过程调用 R 脚本的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ac9537e3e13313e6ca0094a75b0e72c7c8ee80c2
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714756"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>快速入门：SQL Server 中的 "Hello world" R 脚本 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中, 你将通过运行 "Hello World" R 脚本 inT-SQL 来了解关键概念, 并介绍**sp_execute_external_script**系统存储过程。 

## <a name="prerequisites"></a>先决条件

以前的快速入门,[验证 SQL Server 中是否存在 r](quickstart-r-verify.md), 提供了设置本快速入门所需的 R 环境的信息和链接。

## <a name="basic-r-interaction"></a>基本 R 交互

可以通过两种方式在 SQL 数据库中运行 R 代码:

+ 添加 R 脚本作为系统存储过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)的参数。
+ 从[远程 R 客户端](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client)连接到 sql 数据库, 并使用 SQL 数据库作为计算上下文来执行代码。

以下练习重点介绍第一种交互模型: 如何将 R 代码传递到存储过程。

1. 运行简单的脚本, 查看 R 脚本在 SQL 数据库中的执行方式。

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

2. 假设您已正确设置了正确的结果, 并且 R `print`函数将结果返回到 "**消息**" 窗口。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    尽管获取**stdout**消息在测试代码时非常有用, 但更多情况下, 需要以表格格式返回结果, 以便可以在应用程序中使用它或将其写入表中。 请[参阅快速入门:有关详细信息, 请在 SQL Server](rtsql-working-with-inputs-and-outputs.md)中使用 R 处理输入和输出。

请记住, 该参数`@script`内的所有内容都必须是有效的 R 代码。

## <a name="run-a-hello-world-script"></a>运行 Hello World 脚本

以下练习将运行另一个简单的 R 脚本。

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

此存储过程的输入包括:

+ *@language* 参数定义要调用的语言扩展, 在本例中为 R。
+ *@script* 参数定义传递给 R 运行时的命令。 必须以 Unicode 文本形式将整个 R 脚本封装在此参数中。 还可将文本添加到 **nvarchar** 类型的变量并调用该变量。
+ *@input_data_1* 查询返回的数据, 传递给 R 运行时, 它将数据作为数据帧返回 SQL Server。
+ WITH RESULT SETS 子句为 SQL Server 定义返回的数据表的架构, 并将 "Hello World" 添加为列名称, 为数据类型输入**int** 。

**结果**

| 世界您好 |
|-------------|
| 1 |

## <a name="next-steps"></a>后续步骤

现在, 你已运行了几个简单的 R 脚本, 请仔细查看构造输入和输出。

> [!div class="nextstepaction"]
> [起步处理输入和输出](quickstart-r-inputs-and-outputs.md)
