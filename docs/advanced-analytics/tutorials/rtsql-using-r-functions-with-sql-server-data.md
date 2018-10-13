---
title: 快速入门显示 R 函数与 SQL Server 数据 （SQL Server 机器学习） |Microsoft Docs
description: 在本快速入门，了解如何编写使用 SQL Server 数据的 R 函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/08/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 877c7ffd5cb67479eed0e2239cbe90d366934515
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878160"
---
# <a name="quickstart-using-r-functions-with-sql-server-data"></a>快速入门： 使用 SQL Server 数据使用 R 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

如果你在完成上一快速入门教程，您熟悉基本的操作并可供更复杂，例如统计函数。 复杂而无法在 T-SQL 中实现的高级统计函数可以在 R 中使用只有一行代码。

在此快速入门中，将嵌入 R 数学和 SQL Server 中的实用工具函数存储过程。

## <a name="prerequisites"></a>必要條件

上一个快速入门中， [Hello World R 和 SQL 中](rtsql-using-r-code-in-transact-sql-quickstart.md)、 提供的信息和链接设置为本快速入门所需的 R 环境。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>创建一个存储过程来生成随机数字

为简单起见，让我们使用 R`stats`包，其中安装并加载默认情况下，当在 SQL Server 中安装 R 功能支持。 此包中包含数百个用于执行常用统计任务的函数，其中，`rnorm` 函数在给定了标准差和平均数的情况下使用正态分布生成指定数量的随机数字。

例如，以下 R 代码在给定了标准差 3 的情况下返回平均数为 50 的 100 个数字。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

要从 T-SQL 调用此行 R 代码，请运行 sp_execute_external_script 并在 R 脚本参数中添加此 R 函数，如下所示：

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

如果你希望更轻松地生成不同的一组随机数字，那该怎么办？

与 SQL Server 结合使用时轻松达成所愿： 定义从用户获取的参数的存储的过程。 然后，将那些参数作为变量传递给 R 脚本。

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));
```

+ 第一行定义了在执行该存储过程时必需的每个 SQL 输入参数。

+ 以 `@params` 开头的行定义了 R 代码使用的所有变量，以及对应的 SQL 数据类型。

+ 紧跟在后面的行将 SQL 参数名称映射到对应的 R 变量名称。

现在，你已将 R 函数包装在了一个存储过程中，你可以轻松调用该函数并传入不同的值，如下所示：

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 实用工具函数进行故障排除

默认情况下，R 的安装包括`utils`包，可用于调查当前 R 环境中提供的各种实用工具函数。 如果你发现你的 R 代码在 SQL Server 中执行时和在环境外执行时执行方式存在差异，则上述函数会比较有用。

例如，你可以使用 R `memory.limit()` 函数获取当前 R 环境的内存。 因为 `utils` 包默认情况下已安装但未加载，因此你必须首先使用 `library()` 函数加载该包。

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
        library(utils);
        mymemory <- memory.limit();
        OutputDataSet <- as.data.frame(mymemory);'
    , @input_data_1 = N' ;'
WITH RESULT SETS (([Col1] int not null));
```

许多用户喜欢使用的系统计时函数在 R 中，如`system.time`和`proc.time`，以捕获 R 进程使用的时间和分析性能问题。

有关示例，请参阅以下教程：[创建数据功能](../tutorials/walkthrough-create-data-features.md)。 在此演练中，在解决方案中嵌入了 R 计时函数，它们用来对基于数据创建功能的以下两种方法的性能进行比较：R 函数与 T-SQL 函数。

## <a name="next-steps"></a>后续步骤

接下来，你将在 SQL Server 中使用 R 创建一个预测模型。

> [!div class="nextstepaction"]
> [快速入门： 创建预测模型](rtsql-create-a-predictive-model-r.md)
