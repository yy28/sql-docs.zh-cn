---
title: 写入高级 Python 函数
titleSuffix: SQL Server Machine Learning Services
description: 在本快速入门教程中，了解如何使用 SQL Server 机器学习服务为高级统计计算编写 Python 函数。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e369e83c99543cc31287932a25949c2ddec98e89
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007717"
---
# <a name="quickstart-write-advanced-python-functions-with-sql-server-machine-learning-services"></a>快速入门：通过 SQL Server 机器学习服务写入高级 Python 函数
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入门介绍如何使用 SQL Server 机器学习服务在 SQL 存储过程中嵌入 Python 数学和实用函数。 对于在 T-sql 中实现复杂的高级统计函数，只需要一行代码即可在 Python 中完成。

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装了 Python 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 的实例。

  SQL Server 实例可位于 Azure 虚拟机或本地。 请注意，默认情况下禁用外部脚本功能，因此在开始之前，您可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证**SQL Server Launchpad 服务**是否正在运行。

- 还需要一个用于运行包含 Python 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>创建一个存储过程来生成随机数字

为简单起见，我们将使用 Python `numpy` 包，默认情况下，该包安装并加载 SQL Server 安装了 Python 的机器学习服务中。 此包中包含数百个用于执行常用统计任务的函数，其中，`random.normal` 函数在给定了标准差和平均数的情况下使用正态分布生成指定数量的随机数字。

例如，在给定标准偏差为3的50情况下，以下 Python 代码将返回100的平均数。

```Python
numpy.random.normal(size=100, loc=50, scale=3)
```

若要从 T-sql 调用此 Python 行，请在 `sp_execute_external_script` 的 Python 脚本参数中添加 Python 函数。 输出需要一个数据帧，因此使用 `pandas` 来转换它。

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

与 SQL Server 结合起来很简单。 定义从用户获取参数的存储过程，然后将这些参数作为变量传递到 Python 脚本。

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

- 以 `@params` 开头的行定义 Python 代码使用的所有变量，以及相应的 SQL 数据类型。

- 紧跟在后面的行将 SQL 参数名称映射到相应的 Python 变量名称。

既然已将 Python 函数包装在存储过程中，就可以轻松地调用函数并传入不同的值，如下所示：

```sql
EXECUTE MyPyNorm @param1 = 100,@param2 = 50, @param3 = 3
```

## <a name="use-python-utility-functions-for-troubleshooting"></a>使用 Python 实用程序功能进行故障排除

Python 包提供多种实用函数用于调查当前的 Python 环境。 如果在 SQL Server 和外部环境中查找 Python 代码的方式不一致，则这些函数会很有用。

例如，你可能使用 `time` 包中的系统计时函数来度量 Python 进程使用的时间量并分析性能问题。

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

若要在 SQL Server 中使用 Python 创建机器学习模型，请按照以下快速入门：

> [!div class="nextstepaction"]
> [快速入门：使用 SQL Server 机器学习服务 @ no__t 在 Python 中创建和评分预测模型

有关 SQL Server 机器学习服务的详细信息，请参阅：

- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
