---
title: 使用与 revoscalepy Python 创建模型 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: d549b06b9fe371dc2b1966c62776ec4e88c45726
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740826"
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>使用与 revoscalepy Python 创建模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本课程中，你将了解如何从远程开发客户端，在 SQL Server 中创建线性回归模型中运行 Python 代码。 

## <a name="prerequisites"></a>必要條件

+ 本课程中使用不同数据比前面的课程。 不需要先完成前面的课程。 但是，如果你已完成前面的课程中，并且已将服务器已配置为运行 Python，使用该服务器和数据库作为计算上下文。
+ 若要运行 Python 代码使用 SQL Server 作为计算上下文，请要求 2017年或更高版本的 SQL Server。 此外，你必须显式安装，，然后启用功能，**机器学习服务**，选择 Python 语言选项。

    如果你安装 SQL Server 自 2017 年的预发行版本，则应更新到至少的 RTM 版本。 更高版本的服务版本不断扩展和改进 Python 功能。 本教程中的某些功能可能无法在早期的预发行版本。

+ 此示例使用预定义的 Python 环境中，名为`PYTEST_SQL_SERVER`。 配置环境以包含**revoscalepy**和其他所需的库。 

    如果你没有配置为运行 Python 环境，你必须单独执行此操作。 如何创建或修改 Python 环境的讨论不在本教程的范围之内。 有关如何设置包含正确的库的 Python 客户端的详细信息，请参阅[安装 Python 客户端](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)和[到工具的链接 Python](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。

## <a name="remote-compute-contexts-and-revoscalepy"></a>远程计算上下文和 revoscalepy

此示例演示如何在远程创建 Python 模型的过程_计算上下文_，该对话框允许您从客户端，但选择远程环境，如 SQL Server、 Spark 中或计算机学习服务器，其中实际执行的操作。 使用计算上下文，可以更轻松地编写代码一次，并将其部署到任何受支持的环境。

若要在 SQL Server 中执行 Python 代码，需要**revoscalepy**包。 这是由 Microsoft，类似于提供特殊的 Python 包**RevoScaleR** R 语言包。 **Revoscalepy**包支持创建计算上下文，并提供用于在本地工作站和远程服务器之间传递数据和模型的基础结构。 **Revoscalepy**函数的支持的数据库中的代码将执行[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在本课程中，你使用数据中 SQL Server 来训练基于的线性模型[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)中的函数**revoscalepy** ，支持对大型数据集的回归。 

本课还演示如何设置，然后使用的基础知识**SQL Server 计算上下文**Python 中。 有关如何的讨论计算上下文工作与其他平台和其计算上下文支持，请参阅[机器学习 Server 中的脚本执行的计算上下文](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>准备的数据库和示例数据

1. 本课程中使用数据库`sqlpy`。 如果你尚未完成任何前面的课程中，你可以通过运行下面的代码来创建数据库：

    ```sql
    CREATE DATABASE sqlpy;
    GO
    USE sqlpy;
    GO
    ```

    > [!IMPORTANT]
    > 如果你想要使用另一个数据库，一定要编辑的代码示例并将更改连接字符串中的数据库名称。

2. 此示例使用航班数据集，这是在 R 和 Python 中可用。 有关你的 Python 示例创建数据库后，填充包含数据的表，如下所述： [RevoScaleR 中的数据进行采样](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data)。

3. 更改此环境，以便在你的客户端上使用可用环境的名称。

## <a name="run-the-sample-code"></a>运行示例代码

在已准备好数据库，并具有后存储在表中的定型的数据打开 Python 开发环境，并运行的代码示例。

该代码执行以下步骤：

1. 导入所需的库和函数。
2. 创建与 SQL Server 的连接。 创建**数据源**用于使用数据的对象。
3. 修改数据使用**转换**，以便它可以使用逻辑回归算法。
4. 调用`rx_lin_mod`并定义用来拟合模型的公式。
5. 生成一组基于原始数据的预测。
6. 创建基于预测值的摘要。

使用 SQL Server 实例作为计算上下文执行所有操作。

> [!NOTE]
> 有关从命令行运行此示例演示，请观看此视频： [Python 与 SQL Server 自 2017 年高级分析](https://www.youtube.com/watch?v=FcoY795jTcc)

### <a name="sample-code"></a>示例代码

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=sqlpy;Trusted_Connection=True;'
    print("connectionString={0!s}".format(sql_connection_string))

    data_source = RxSqlServerData(
        sql_query = "select top 10 * from airlinedemosmall",
        connection_string = sql_connection_string,

        column_info = {
            "ArrDelay" : { "type" : "integer" },
            "DayOfWeek" : {
                "type" : "factor",
                "levels" : [ "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday" ]
            }
        })

    sql_compute_context = RxInSqlServer(
        connection_string = sql_connection_string,
        num_tasks = 4,
        auto_cleanup = False
        )

    #
    # Run linmod locally
    #
    linmod_local = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source)
    #
    # Run linmod remotely
    #
    linmod = rx_lin_mod("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)

    # Predict results
    # 
    predict = rx_predict(linmod, data = rx_import(input_data = data_source))
    summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)
```

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>定义了一个数据源与定义的计算上下文

数据源是不同的计算上下文。 _数据源_定义在代码中使用的数据。 _计算上下文_定义才能执行的代码。 但是，它们使用的一些相同的信息：

+ Python 变量，如`sql_query`和`sql_connection_string`，定义的数据源。 

    将对这些变量传递[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)构造函数来实现**数据源对象**名为`data_source`。

+ 你创建**计算上下文对象**使用[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata)构造函数。 生成**计算上下文对象**名为`sql_cc`。

    此示例重新在数据源中，假定你将使用作为计算上下文的相同 SQL Server 实例上的数据是使用与你使用相同的连接字符串。 
    
    但是，数据源和计算上下文可能在不同服务器上。
 
### <a name="changing-compute-contexts"></a>更改计算上下文

定义计算上下文之后，必须设置**主动计算上下文**。 

默认情况下，大多数操作在本地运行，这意味着，如果没有指定不同的计算上下文，将从数据源提取数据的代码将在你当前的 Python 环境中运行。

有两种方法设置的主动计算上下文：
+ 作为方法或函数的自变量
+ 通过调用 `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>作为方法或函数的自变量设置计算上下文

你可以在此示例中，来设置使用的单个自变量计算上下文**rx**函数。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

在调用中重用此计算上下文[rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):。

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>设置显式使用 rx_set_compute_context 的计算上下文

该函数[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)允许之间切换计算已定义的上下文。

设置之后活动计算上下文，在更改之前，它保持活动状态。

### <a name="using-parallel-processing-and-streaming"></a>使用并行处理和流式处理

当你定义的计算上下文时，你还可以设置参数计算上下文中的数据的处理方式该控件。 这些参数与不同，具体取决于数据源类型。

对于 SQL Server 计算上下文，你可以设置批大小，或提供有关要在正在运行的任务中使用的并行度提示。

+ 具有四个处理器的计算机上运行示例的因此`num_tasks`参数设置为 4，以允许最大资源使用。 
+ 如果此值设置为 0 时，SQL Server 将使用默认设置，即能够尽可能情况下，在服务器的当前 MAXDOP 设置并行运行多个任务。 但是，可能会分配的任务的精确数目取决于许多其他因素，如服务器设置和运行其他作业。

## <a name="related-samples"></a>相关的示例

这些其他的 Python 示例和教程演示使用更复杂的数据源，以及远程计算上下文使用的端到端方案。

+ [SQL 开发人员的数据库中 Python](sqldev-in-database-python-for-sql-developers.md)
+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
