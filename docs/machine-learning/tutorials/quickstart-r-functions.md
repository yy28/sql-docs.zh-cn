---
title: 快速入门：R 函数
description: 本快速入门介绍如何通过 SQL Server 机器学习服务使用 R 数学和实用工具函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fd3c3326fe0b186ade24cbcf95f587abba1cb6bc
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487273"
---
# <a name="quickstart-r-functions-with-sql-server-machine-learning-services"></a>快速入门：SQL Server 机器学习服务中的 R 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入门介绍如何通过 SQL Server 机器学习服务使用 R 数学和实用工具函数。 通常在 T-SQL 中难以实现的统计函数在 R 中只需几行代码就可以实现。

## <a name="prerequisites"></a>先决条件

- 本快速入门需要使用安装了 R 语言的 [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 实例。

  SQL Server 实例可以位于 Azure 虚拟机中，也可以位于本地。 请注意，默认情况下禁用外部脚本编写功能，因此可能需要在开始之前[启用外部脚本编写](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证 SQL Server Launchpad 服务是否正在运行  。

- 你还需要一个工具来运行包含 R 脚本的 SQL 查询。 可使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，并运行 T-SQL 查询或存储过程即可。 本快速入门使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>创建一个存储过程来生成随机数字

为简单起见，让我们使用 R `stats` 包，此包默认安装并加载到装有 R 的 SQL Server 机器学习服务中。 此包中包含数百个用于执行常用统计任务的函数，其中，`rnorm` 函数在给定了标准差和平均数的情况下使用正态分布生成指定数量的随机数字。

例如，以下 R 代码在标准偏差为 3 的情况下返回平均值为 50 的 100 个数字。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

若要从 T-SQL 调用此行 R 代码，请在 `sp_execute_external_script` 的 R 脚本参数中添加此 R 函数，如下所示：

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

如果你希望更轻松地生成不同的一组随机数字，那该怎么办？

与 SQL Server 结合使用时操作非常简单。 定义一个存储过程，从用户那里获取参数，然后将这些参数作为变量传递给 R 脚本。

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 第一行定义了在执行该存储过程时必需的每个 SQL 输入参数。

- 以 `@params` 开头的行定义了 R 代码使用的所有变量，以及对应的 SQL 数据类型。

- 紧跟在后面的行将 SQL 参数名称映射到对应的 R 变量名称。

现在，你已将 R 函数包装在了一个存储过程中，你可以轻松调用该函数并传入不同的值，如下所示：

```sql
EXECUTE MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 实用工具函数进行故障排除

默认安装的 **utils** 包提供各种实用工具函数来调查当前 R 环境。 如果你发现 R 代码在 SQL Server 和外部环境中的执行方式存在差异，那么这些函数会很有用。

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

> [!TIP]
> 许多用户喜欢使用 R 中的系统计时函数（例如 `system.time` 和 `proc.time`）来捕获 R 进程使用的时间并分析性能问题。 有关示例，请参阅教程[创建数据特征](../tutorials/walkthrough-create-data-features.md)，其中的解决方案嵌入了 R 计时函数。

## <a name="next-steps"></a>后续步骤

若要在 SQL Server 中使用 R 创建机器学习模型，请遵循以下快速入门：

> [!div class="nextstepaction"]
> [通过 SQL Server 机器学习服务在 R 中创建预测模型并对其进行评分](quickstart-r-train-score-model.md)

有关 SQL Server 机器学习服务的详细信息，请参阅：

- [什么是 SQL Server 机器学习服务（Python 和 R）？](../sql-server-machine-learning-services.md)
