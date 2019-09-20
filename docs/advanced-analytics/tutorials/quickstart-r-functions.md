---
title: 编写高级 R 函数
titleSuffix: SQL Server Machine Learning Services
description: 本快速入门介绍如何使用 SQL Server 机器学习服务为高级统计计算编写 R 函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: cebd4ea6a356af6802a0e26f778667b2acc4b80c
ms.sourcegitcommit: 1661c3e1bb38ed12f8485c3860fc2d2b97dd2c9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/20/2019
ms.locfileid: "71149910"
---
# <a name="quickstart-write-advanced-r-functions-with-sql-server-machine-learning-services"></a>快速入门：通过 SQL Server 机器学习服务写入高级 R 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入门介绍如何使用 SQL Server 机器学习服务在 SQL 存储过程中嵌入 R 数学和实用函数。 在 T-sql 中实现复杂的高级统计函数可在 R 中完成，只需要一行代码。

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装 R 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)SQL Server 的实例。

  SQL Server 实例可位于 Azure 虚拟机或本地。 请注意，默认情况下禁用外部脚本功能，因此在开始之前，您可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证**SQL Server Launchpad 服务**是否正在运行。

- 还需要一个用于运行包含 R 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>创建一个存储过程来生成随机数字

为简单起见，我们使用 r 包`stats` ，默认情况下，在安装了 r 的 SQL Server 机器学习服务中安装和加载了 r 包。 此包中包含数百个用于执行常用统计任务的函数，其中，`rnorm` 函数在给定了标准差和平均数的情况下使用正态分布生成指定数量的随机数字。

例如，在给定标准偏差为3的50情况下，以下 R 代码将返回100的平均值。

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

若要从 t-sql 调用此 r 行，请在的`sp_execute_external_script`r 脚本参数中添加 r 函数，如下所示：

```sql
EXEC sp_execute_external_script
      @language = N'R'
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'
    , @input_data_1 = N'   ;'
      WITH RESULT SETS (([Density] float NOT NULL));
```

如果你希望更轻松地生成不同的一组随机数字，那该怎么办？

与 SQL Server 结合起来很简单。 定义从用户获取参数的存储过程，然后将这些参数作为变量传递给 R 脚本。

```sql
CREATE PROCEDURE MyRNorm (
    @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXEC sp_execute_external_script @language = N'R'
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
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 实用工具函数进行故障排除

默认情况下，安装的**utils**包提供了各种用于调查当前 R 环境的实用函数。 如果在 SQL Server 和外部环境中执行 R 代码的方式不一致，则这些函数会很有用。

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
> 许多用户喜欢使用 r 中的系统计时函数（如`system.time`和`proc.time`）来捕获 r 进程使用的时间，并分析性能问题。

有关示例，请参阅本教程：[创建数据功能](../tutorials/walkthrough-create-data-features.md)。 在本演练中，R 计时函数嵌入在解决方案中，用于比较 R 函数与用于从数据创建功能的 t-sql 函数。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 机器学习服务的详细信息，请参阅：

- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
