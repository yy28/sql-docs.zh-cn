---
title: "\"Hello World\"基本 R 代码执行的 T-SQL 的 SQL Server 机器学习中的快速入门"
description: SQL Server 中的 R 脚本的快速入门。 了解调用 R 脚本在你好 world 练习使用 sp_execute_external_script 系统存储过程的基础知识。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1ec9580a533e51b7e99ea0ac34c1d322a27da452
ms.sourcegitcommit: 3cfedfeba377560d460ca3e42af1e18824988c07
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2019
ms.locfileid: "59042272"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>快速入门：SQL Server 中的"hello world"R 脚本 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本快速入门教程，了解关键概念，通过运行"Hello World"R 脚本 inT SQL，简介**sp_execute_external_script**系统存储过程。 

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 R](quickstart-r-verify.md)、 提供的信息和链接设置为本快速入门所需的 R 环境。

## <a name="basic-r-interaction"></a>基本 R 交互

有两种方法可以在 SQL 数据库中运行 R 代码：

+ 系统存储过程的参数添加 R 脚本[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。
+ 从[远程 R 客户端](https://docs.microsoft.com/sql/advanced-analytics/r/set-up-a-data-science-client)，连接到 SQL 数据库，并使用 SQL 数据库作为计算上下文执行代码。

以下练习的重点是第一个交互模型： 如何将 R 代码传递给存储过程。

1. 运行简单的脚本，以查看 R 脚本在 SQL 数据库中的执行方式。

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'R',
    @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))'
    '
    ```

2. 假设你有完成所有设置正确正确的结果进行计算，和 R`print`函数将返回到结果**消息**窗口。

    **结果**

    ```text
    STDOUT message(s) from external script: 
    0.5 2
    ```

    获取时**stdout**测试你的代码时，消息很有用，更频繁地需要以表格格式返回结果，以便可以在应用程序中使用它或将其写入到一个表。 请参阅[快速入门：句柄输入和输出在 SQL Server 中使用 R](rtsql-working-with-inputs-and-outputs.md)有关详细信息。

请记住内的所有内容`@script`参数必须是有效的 R 代码。

## <a name="run-a-hello-world-script"></a>运行 Hello World 脚本

以下练习中运行另一个简单的 R 脚本。

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'OutputDataSet<-InputDataSet',
  @input_data_1 =N'SELECT 1 AS hello'
  WITH RESULT SETS (([Hello World] int));
GO
```

此存储过程的输入包括：

+ *@language* 参数定义的语言扩展。 若要调用，在这种情况下，。
+ *@script* 参数定义传递给 R 运行时的命令。 必须以 Unicode 文本形式将整个 R 脚本封装在此参数中。 还可将文本添加到 **nvarchar** 类型的变量并调用该变量。
+ *@input_data_1* 该查询中，传递给 R 运行时，将数据返回到 SQL Server 作为数据帧返回数据。
+ 使用结果集子句返回的数据的表的架构定义的 SQL Server，将"Hello World"添加列名称，为**int**的数据类型。

**结果**

| 世界您好 |
|-------------|
| 1 |

## <a name="next-steps"></a>后续步骤

现在，已运行几个简单的 R 脚本，需要深入研究构建输入和输出。

> [!div class="nextstepaction"]
> [快速入门：处理输入和输出](quickstart-r-inputs-and-outputs.md)
