---
title: 将 Python 与使用 revoscalepy 创建模型 |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 5c8ff387c3abda3f147700dce6349009a027a778
ms.sourcegitcommit: 3cd6068f3baf434a4a8074ba67223899e77a690b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2018
ms.locfileid: "49461953"
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>将 Python 与使用 revoscalepy 创建模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在本课程中，您将学习如何从远程开发客户端，若要在 SQL Server 中创建线性回归模型中运行 Python 代码。 

## <a name="prerequisites"></a>必要條件

+ 本课程中使用不同的数据比前面的课程。 不需要先完成前面的课程。 但是，如果你已完成前面的课程，并且可以将服务器已配置为运行 Python，使用该服务器和数据库作为计算上下文。
+ 若要运行 Python 代码使用 SQL Server 作为计算上下文需要 SQL Server 2017 或更高版本。 此外，必须显式安装并启用该功能，然后**机器学习服务**，选择 Python 语言选项。

    如果您安装 SQL Server 2017 的预发布版本，您应至少更新到 RTM 版本。 更高版本的 service release 不断扩展和改进 Python 功能。 本教程中的某些功能可能无法在早期预发布版本。

+ 此示例使用预定义的 Python 环境，名为`PYTEST_SQL_SERVER`。 配置环境以包含**revoscalepy**和其他所需的库。 

    如果没有配置为运行 Python 环境，你必须单独执行。 如何创建或修改 Python 环境的讨论不在本教程的范围之内。 有关如何设置包含正确的库的 Python 客户端的详细信息，请参阅[安装 Python 客户端](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)并[工具的链接 Python](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)。

## <a name="remote-compute-contexts-and-revoscalepy"></a>远程计算上下文并 revoscalepy

此示例演示如何在远程创建 Python 模型的过程_计算上下文_，它允许您从客户端，但选择远程环境，如 SQL Server、 Spark 或机器学习服务器位置实际执行的操作。 使用计算上下文，可以更轻松地编写代码一次，并将其部署到任何受支持的环境。

若要在 SQL Server 中执行 Python 代码，需要**revoscalepy**包。 这是类似于 Microsoft 提供的特殊 Python 软件包**RevoScaleR**的 R 语言包。 **Revoscalepy**包支持创建计算上下文，并提供用于在本地工作站和远程服务器之间传递数据和模型的基础结构。 **Revoscalepy**函数在数据库中的代码执行是的支持[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在本课程中，可以使用数据在 SQL Server 中基于线性模型进行定型[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)中的函数**revoscalepy**通过极大型数据集支持回归。 

本课程还演示了如何设置以及如何将的基础知识**SQL Server 计算上下文**Python 中。 有关介绍如何计算上下文工作与其他平台，以及哪个计算上下文支持，请参阅[机器学习服务器中的脚本执行的计算上下文](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)

## <a name="prepare-the-database-and-sample-data"></a>准备数据库和示例数据

1. 本课程中使用的数据库**sqlpy**。 如果未完成任何前面的课程，您可以通过运行以下代码创建数据库：

    ```sql
    CREATE DATABASE sqlpy;
    GO
    USE sqlpy;
    GO
    ```

    > [!IMPORTANT]
    > 如果你想要使用不同的数据库，请确保要编辑的示例代码并更改连接字符串中的数据库名称。

2. 此示例使用航班数据集，这是 R 和 Python 中可用。 有关 Python 示例创建数据库后，填充包含数据的表，如下所述： [RevoScaleR 中的数据采样](https://docs.microsoft.com/machine-learning-server/r/sample-built-in-data)。

3. 更改此环境以使用在客户端上的可用环境的名称。

## <a name="run-the-sample-code"></a>运行示例代码

已准备好数据库并且具有后存储在表中，定型的数据打开 Python 开发环境和运行代码示例。

该代码执行以下步骤：

1. 导入所需的库和函数。
2. 创建到 SQL Server 的连接。 创建**数据源**用于处理数据的对象。
3. 修改数据使用**转换**，以便它可以使用逻辑回归算法。
4. 调用`rx_lin_mod`并定义用来拟合模型的公式。
5. 生成一组基于原始数据的预测。
6. 创建基于预测值的摘要。

使用 SQL Server 的实例作为计算上下文执行所有操作。

> [!NOTE]
> 从命令行运行此示例的演示，请参阅此视频：[与 Python 配合使用 SQL Server 2017 高级分析](https://www.youtube.com/watch?v=FcoY795jTcc)

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

### <a name="defining-a-data-source-vs-defining-a-compute-context"></a>定义数据源与定义计算上下文

数据源与不同计算上下文。 _数据源_定义在代码中使用的数据。 _计算上下文_定义执行代码的位置。 但是，它们使用的一些相同的信息：

+ Python 变量，如`sql_query`和`sql_connection_string`，定义的数据源。 

    将对这些变量传递[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)构造函数来实现**数据源对象**名为`data_source`。

+ 您创建**计算上下文对象**通过使用[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata)构造函数。 得到**计算上下文对象**名为`sql_cc`。

    此示例在数据源中，假定您将使用作为计算上下文的同一 SQL Server 实例上的数据重新使用所用的相同连接字符串。 
    
    但是，数据源和计算上下文可以位于不同服务器上。
 
### <a name="changing-compute-contexts"></a>更改计算上下文

定义计算上下文后，必须设置**活动的计算上下文**。 

默认情况下，大多数操作在本地运行，这意味着，如果未指定不同的计算上下文，将从数据源提取的数据和代码将在当前 Python 环境中运行。

有两种方法来设置活动计算上下文：
+ 作为方法或函数的参数
+ 通过调用 `rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>作为方法或函数的参数设置计算上下文

通过使用个人的参数在此示例中，设置计算上下文**rx**函数。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

在调用中重用此计算上下文[rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):。

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>设置计算上下文显式使用 rx_set_compute_context

该函数[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)允许之间切换计算上下文已定义的。

设置后活动计算上下文，在更改之前将其保持活动状态。

### <a name="using-parallel-processing-and-streaming"></a>使用并行处理和流式处理

在定义计算上下文时，您还可以设置参数的计算上下文如何处理数据的控件。 这些参数的数据源类型而异。

对于 SQL Server 计算上下文，可以设置批大小，或提供有关要在正在运行的任务中使用的并行度提示。

+ 具有四个处理器的计算机上运行该示例的因此`num_tasks`参数设置为 4，以便最充分地利用资源。 
+ 如果此值设置为 0 时，SQL Server 将使用默认情况下，它将在当前的 MAXDOP 设置为服务器下尽可能以并行方式运行那么多的任务。 但是，可能会分配的任务的精确数目取决于许多其他因素，如服务器设置和其他正在运行的作业。

## <a name="related-samples"></a>相关的示例

这些其他的 Python 示例和教程演示使用更复杂的数据源，以及使用远程计算上下文的端到端方案。

+ [面向 SQL 开发人员的数据库 Python](sqldev-in-database-python-for-sql-developers.md)
+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
