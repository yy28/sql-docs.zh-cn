---
title: 将 Python 与 revoscalepy 配合使用来创建模型
description: 使用 revoscalepy 函数编写 Python 脚本, 以创建远程运行在 SQL Server 中的数据科学模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 3fe398a6210936553fc40b10cc9a42f395a98785
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345803"
---
# <a name="use-python-with-revoscalepy-to-create-a-model-that-runs-remotely-on-sql-server"></a>将 Python 与 revoscalepy 配合使用, 创建在 SQL Server 上远程运行的模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft 的[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) Python 库为数据浏览、可视化、转换和分析提供数据科学算法。 此库在 SQL Server 的 Python 集成方案中具有战略性的重要性。 在多核服务器上, **revoscalepy**函数可并行运行。 在包含中央服务器和客户端工作站 (单独的物理计算机, 具有相同的**revoscalepy**库) 的分布式体系结构中, 你可以编写在本地启动的 Python 代码, 然后将执行转移到远程 SQL Server 实例数据驻留的位置。

可以在以下 Microsoft 产品和分发中找到**revoscalepy** :

+ [SQL Server 机器学习服务 (数据库内)](../install/sql-machine-learning-services-windows-install.md)
+ [Microsoft Machine Learning Server (非 SQL, 独立服务器)](https://docs.microsoft.com/machine-learning-server/index)
+ [客户端 Python 库 (适用于开发工作站)](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter) 

本练习演示了如何基于[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)创建线性回归模型, 该模型是一种接受计算上下文作为输入的**revoscalepy**算法。 你将在本练习中运行的代码将从本地到远程计算环境 (由启用远程计算上下文的**revoscalepy**函数启用) 中进行代码执行。

完成本教程后, 你将学习如何执行以下操作:

> [!div class="checklist"]
> * 使用**revoscalepy**创建线性模型
> * 从本地到远程计算上下文的移位操作

## <a name="prerequisites"></a>先决条件

此练习中使用的示例数据是[**flightdata**](demo-data-airlinedemo-in-sql.md)数据库。

若要运行本文中的示例代码, 必须将 ide 链接到 Python 可执行文件。

若要练习计算上下文班次, 需要启用了[机器学习服务](../install/sql-machine-learning-services-windows-install.md)和 Python 的[本地工作站](../python/setup-python-client-tools-sql.md)和 SQL Server 数据库引擎实例。 

> [!Tip]
> 如果没有两台计算机, 则可以通过安装相关的应用程序在一台物理计算机上模拟远程计算上下文。 首先, 安装[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)以 "远程" 实例的方式运行。 其次, 安装[Python 客户端库的操作](../python/setup-python-client-tools-sql.md)是客户端。 同一台计算机上将有两个相同 Python 分发和 Microsoft Python 库的副本。 你需要跟踪文件路径, 以及你使用哪一个 Python 来成功完成练习。

## <a name="remote-compute-contexts-and-revoscalepy"></a>远程计算上下文和 revoscalepy

此示例演示在远程计算上下文中创建 Python 模型的过程, 该过程可让你从客户端进行工作, 但请选择在其中实际执行操作的远程环境, 例如 SQL Server、Spark 或 Machine Learning Server。 远程计算上下文的目标是将计算引入到数据所在的位置。

若要在 SQL Server 中执行 Python 代码, 需要**revoscalepy**包。 这是 Microsoft 提供的一种特殊 Python 包, 类似于 R 语言的**RevoScaleR**包。 **Revoscalepy**包支持创建计算上下文, 并提供用于在本地工作站与远程服务器之间传递数据和模型的基础结构。 支持数据库内代码执行的**revoscalepy**函数为[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)。

在本课程中, 您将使用 SQL Server 中的数据, 根据[rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)( **revoscalepy**中支持对非常大的数据集的回归的函数) 训练线性模型。 

本课还演示了如何在 Python 中设置和使用**SQL Server 计算上下文**的基础知识。 有关计算上下文如何与其他平台一起工作以及支持哪些计算上下文的讨论, 请参阅[Machine Learning Server 中脚本执行的计算上下文](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-compute-context)。


## <a name="run-the-sample-code"></a>运行示例代码

准备好数据库并将定型数据存储在表中后, 打开 Python 开发环境并运行代码示例。

此代码执行以下步骤:

1. 导入所需的库和函数。
2. 创建与 SQL Server 的连接。 创建用于处理数据的**数据源**对象。
3. 使用**转换**来修改数据, 使其可供逻辑回归算法使用。
4. 调用`rx_lin_mod`并定义用于拟合模型的公式。
5. 基于原始数据生成一组预测。
6. 基于预测值创建汇总。

所有操作都使用 SQL Server 的实例作为计算上下文来执行。

> [!NOTE]
> 若要从命令行运行此示例的演示, 请观看此视频:[通过 Python SQL Server 2017 高级分析](https://www.youtube.com/watch?v=FcoY795jTcc)

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

数据源不同于计算上下文。 *数据源*定义代码中使用的数据。 计算上下文定义将执行代码的位置。 但是, 它们使用的信息如下:

+ Python 变量 (例如`sql_query`和`sql_connection_string`) 定义数据源。 

    将这些变量传递给[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)构造函数以实现名为`data_source`的**数据源对象**。

+ 您可以使用[RxInSqlServer](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rxinsqlserver)构造函数创建**计算上下文对象**。 生成的**计算上下文对象**命名为`sql_cc`。

    此示例将使用您在数据源中使用的相同连接字符串, 假设数据位于将用作计算上下文的相同 SQL Server 实例上。 
    
    但是, 数据源和计算上下文可能位于不同的服务器上。
 
### <a name="changing-compute-contexts"></a>更改计算上下文

定义计算上下文后, 必须设置**活动计算上下文**。 

默认情况下, 大多数操作都在本地运行, 这意味着, 如果未指定其他计算上下文, 则将从数据源中提取数据, 代码将在当前的 Python 环境中运行。

可以通过两种方式设置活动计算上下文:
+ 作为方法或函数的参数
+ 通过调用`rx_set_computecontext`

#### <a name="set-compute-context-as-an-argument-of-a-method-or-function"></a>将计算上下文设置为方法或函数的参数

在此示例中, 您使用单个**rx**函数的参数设置计算上下文。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

在对[rxsummary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)的调用中重复使用此计算上下文:

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

#### <a name="set-a-compute-context-explicitly-using-rxsetcomputecontext"></a>使用 rx_set_compute_context 显式设置计算上下文

函数[rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context)使您能够在已定义的计算上下文之间切换。

设置活动计算上下文后, 它将一直保持活动状态, 直到您对其进行更改。

### <a name="using-parallel-processing-and-streaming"></a>使用并行处理和流式处理

定义计算上下文时, 还可以设置用于控制计算上下文如何处理数据的参数。 这些参数因数据源类型而异。

对于 SQL Server 计算上下文, 你可以设置批大小, 或者提供有关要在运行任务中使用的并行度的提示。

+ 该示例在具有四个处理器的计算机上运行, 因此`num_tasks` , 参数设置为4以允许最大限度地利用资源。 
+ 如果将此值设置为 0, SQL Server 将使用默认值, 该默认值是在服务器的当前 MAXDOP 设置下并行运行尽可能多的任务。 但是, 可能分配的任务的确切数目取决于许多其他因素, 如服务器设置和运行的其他作业。

## <a name="next-steps"></a>后续步骤

这些附加的 Python 示例和教程演示了使用更复杂的数据源的端到端方案, 以及使用远程计算上下文的情况。

+ [面向 SQL 开发人员的数据库内 Python](sqldev-in-database-python-for-sql-developers.md)
+ [使用 Python 和 SQL Server 构建预测模型](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
