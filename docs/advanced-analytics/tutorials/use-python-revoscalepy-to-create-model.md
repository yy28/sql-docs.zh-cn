---
title: 将 Python 与 revoscalepy 使用在 SQL Server 中创建模型 |Microsoft Docs
description: 编写使用 revoscalepy 函数来创建在 SQL Server 中远程运行的数据科学模型的 Python 脚本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: f554badcba282bad7fb386daf8c4c0f4106804b4
ms.sourcegitcommit: 9f2edcdf958e6afce9a09fb2e572ae36dfe9edb0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2018
ms.locfileid: "50100158"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>将 Python 与使用 revoscalepy 创建模型的 SQL Server 上远程运行
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[Revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)来自 Microsoft 的 Python 库提供了数据科学算法用于数据浏览、 可视化效果、 转换和分析。 此库中的 Python 集成方案中 SQL Server 具有战略的重要性。 在多核服务器上， **revoscalepy**函数可以并行运行。 在分布式体系结构中使用中央服务器和客户端工作站 (单独的物理计算机，所有具有相同**revoscalepy**库)，可以编写的本地启动，但然后转移到执行 Python 代码数据所在的远程 SQL Server 实例。

您可以找到**revoscalepy**以下 Microsoft 产品和发行版中：

+ [SQL Server 机器学习服务 （数据库内）](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft 机器学习服务器 （非 SQL、 独立服务器）](https://docs.microsoft.com/machine-learning-server/index)
+ [（适用于开发工作站） 的客户端的 Python 库](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

此练习将演示如何创建线性回归模型基于[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)中的算法之一**revoscalepy**接受作为输入的计算上下文。 在此练习中将运行的代码会执行代码从本地切换到远程计算环境中，通过启用**revoscalepy**函数启用远程计算上下文。

通过完成本教程中，您将学习如何：

> [!div class="checklist"]
> * 使用**revoscalepy**若要创建一个线性模型
> * 将操作从本地切换到远程计算上下文

## <a name="prerequisites"></a>必要條件

在此练习中使用的示例数据[ **flightdata** ](demo-data-airlinedemo-in-sql.md)数据库。

您需要 IDE，可在本文中，运行示例代码和 IDE 必须链接到 Python 可执行文件。

若要练习计算上下文 shift，需要[本地工作站](../python/setup-python-client-tools-sql.md)和 SQL Server 数据库引擎实例与[机器学习服务](../install/sql-machine-learning-services-windows-install.md)和启用了 Python。 

> [!Tip]
> 如果你没有两台计算机，你可以通过安装相关的应用程序模拟一个物理计算机上的远程计算上下文。 首先，安装[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)作为"远程"的实例进行操作。 第二个，安装了[Python 客户端库运行](../python/setup-python-client-tools-sql.md)与客户端。 将具有相同的 Python 分发版和 Microsoft Python 库在同一台计算机上的两个副本。 必须将跟踪的文件路径和用来成功完成该练习的 Python.exe 的哪一副本。

## <a name="remote-compute-contexts-and-revoscalepy"></a>远程计算上下文并 revoscalepy

此示例演示了创建 Python 模型在远程计算上下文中，该对话框允许您从客户端，但选择远程环境，如 SQL Server、 Spark 或机器学习服务器，实际执行的操作的过程。 远程计算上下文的目的是使计算到数据所在的位置。

若要在 SQL Server 中执行 Python 代码，需要**revoscalepy**包。 这是类似于 Microsoft 提供的特殊 Python 软件包**RevoScaleR**的 R 语言包。 **Revoscalepy**包支持创建计算上下文，并提供用于在本地工作站和远程服务器之间传递数据和模型的基础结构。 **Revoscalepy**函数在数据库中的代码执行是的支持[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在本课程中，可以使用数据在 SQL Server 中基于线性模型进行定型[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)中的函数**revoscalepy**通过极大型数据集支持回归。 

本课程还演示了如何设置以及如何将的基础知识**SQL Server 计算上下文**Python 中。 有关介绍如何计算上下文工作与其他平台，以及哪个计算上下文支持，请参阅[机器学习服务器中的脚本执行的计算上下文](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。


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

数据源与不同计算上下文。 *数据源*定义在代码中使用的数据。 计算上下文定义执行代码的位置。 但是，它们使用的一些相同的信息：

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

在调用中重用此计算上下文[rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary):

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>设置计算上下文显式使用 rx_set_compute_context

该函数[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)允许之间切换计算上下文已定义的。

设置后活动计算上下文，在更改之前将其保持活动状态。

### <a name="using-parallel-processing-and-streaming"></a>使用并行处理和流式处理

在定义计算上下文时，您还可以设置参数的计算上下文如何处理数据的控件。 这些参数的数据源类型而异。

对于 SQL Server 计算上下文，可以设置批大小，或提供有关要在正在运行的任务中使用的并行度提示。

+ 具有四个处理器的计算机上运行该示例的因此`num_tasks`参数设置为 4，以便最充分地利用资源。 
+ 如果此值设置为 0 时，SQL Server 将使用默认情况下，它将在当前的 MAXDOP 设置为服务器下尽可能以并行方式运行那么多的任务。 但是，可能会分配的任务的精确数目取决于许多其他因素，如服务器设置和其他正在运行的作业。

## <a name="next-steps"></a>后续步骤

这些其他的 Python 示例和教程演示使用更复杂的数据源，以及使用远程计算上下文的端到端方案。

+ [面向 SQL 开发人员的数据库 Python](sqldev-in-database-python-for-sql-developers.md)
+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
