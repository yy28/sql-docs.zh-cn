---
title: 快速入门：Python 函数
description: 本快速入门介绍了如何将 Python 数学和实用工具函数与 SQL Server 机器学习服务结合使用。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/28/2020
ms.topic: quickstart
author: cawrites
ms.author: chadam
ms.reviewer: garye
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6afe1685956c43e30ace59f3e5cc794a2abbd88f
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606696"
---
# <a name="quickstart-python-functions-with-sql-server-machine-learning-services"></a>快速入门：结合使用 Python 函数和 SQL Server 机器学习服务
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
本快速入门介绍如何在 [SQL Server 机器学习服务](../sql-server-machine-learning-services.md)中或[大数据群集](../../big-data-cluster/machine-learning-services.md)上使用 Python 数学和实用程序函数。 统计函数在 T-SQL 中实现起来通常很复杂，但在 Python 中只需几行代码就可以完成。
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
本快速入门介绍如何将 Python 数学和实用程序函数与 [SQL Server 机器学习服务](../sql-server-machine-learning-services.md)结合使用。 统计函数在 T-SQL 中实现起来通常很复杂，但在 Python 中只需几行代码就可以完成。
::: moniker-end

## <a name="prerequisites"></a>先决条件

- 本快速入门需要使用安装了 Python 语言的 [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 实例。

  SQL Server 实例可以位于 Azure 虚拟机中，也可以位于本地。 请注意，默认情况下禁用外部脚本编写功能，因此可能需要在开始之前[启用外部脚本编写](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证 SQL Server Launchpad 服务是否正在运行。

- 你还需要一个工具来运行包含 Python 脚本的 SQL 查询。 可使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，并运行 T-SQL 查询或存储过程即可。 本快速入门使用 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio)。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>创建一个存储过程来生成随机数字

为简单起见，使用 Python `numpy` 包，该包是在安装了 Python 的 SQL Server 机器学习服务的情况下默认安装和加载的。 此包中包含数百个用于执行常用统计任务的函数，其中，`random.normal` 函数在给定了标准差和平均数的情况下使用正态分布生成指定数量的随机数字。

例如，以下 Python 代码在给定了标准差 3 的情况下返回平均数为 50 的 100 个数字。

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

若要从 T-SQL 调用此行 Python，请在 `sp_execute_external_script` 的 Python 脚本参数中添加 Python 函数。 输出需要一个数据帧，因此使用 `pandas` 来转换它。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=100, loc=50, scale=3));
'
    , @input_data_1 = N'   ;'
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

如果你希望更轻松地生成不同的一组随机数字，那该怎么办？

与 SQL Server 结合使用时操作非常简单。 定义一个存储过程，从用户那里获取参数，然后将这些参数作为变量传递给 Python 脚本。

```sql
CREATE PROCEDURE MyPyNorm (
      @param1 INT
    , @param2 INT
    , @param3 INT
    )
AS
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import numpy
import pandas
OutputDataSet = pandas.DataFrame(numpy.random.normal(size=mynumbers, loc=mymean, scale=mysd));
'
    , @input_data_1 = N'   ;'
    , @params = N' @mynumbers int, @mymean int, @mysd int'
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
WITH RESULT SETS(([Density] FLOAT NOT NULL));
```

- 第一行定义了在执行该存储过程时必需的每个 SQL 输入参数。

- 以 `@params` 开头的行定义了 Python 代码使用的所有变量，以及对应的 SQL 数据类型。

- 紧跟在后面的行将 SQL 参数名称映射到对应的 Python 变量名称。

现在，你已将 Python 函数包装在了一个存储过程中，轻松调用该函数并传入不同的值，如下所示：

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>使用 Python 实用工具函数进行故障排除

Python 包提供了多种实用函数来调查当前的 Python 环境。 如果你发现 Python 代码在 SQL Server 中执行时和在环境外执行时执行方式存在差异，则上述函数会比较有用。

例如，你可以使用 `time` 包中的系统计时函数来测量 Python 进程使用的时间量并分析性能问题。

```sql
EXECUTE sp_execute_external_script
      @language = N'Python'
    , @script = N'
import time
start_time = time.time()

# Run Python processes

elapsed_time = time.time() - start_time
'
    , @input_data_1 = N' ;';
```

## <a name="next-steps"></a>后续步骤

若要在 SQL Server 中使用 Python 创建机器学习模型，请遵循以下快速入门：

> [!div class="nextstepaction"]
> [快速入门：通过 SQL Server 机器学习服务在 Python 中创建预测模型并对其进行评分](quickstart-python-train-score-model.md)

有关 SQL Server 机器学习服务的详细信息，请参阅：

- [什么是 SQL Server 机器学习服务（Python 和 R）？](../sql-server-machine-learning-services.md)
