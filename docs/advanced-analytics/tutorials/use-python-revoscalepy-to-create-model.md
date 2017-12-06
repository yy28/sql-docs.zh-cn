---
title: "使用与 revoscalepy Python 创建模型 |Microsoft 文档"
ms.custom: SQL2016_New_Updated
ms.date: 09/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: bb5d4aac51728ac090fb4cbeae8da6c87db22aea
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="use-python-with-revoscalepy-to-create-a-model"></a>使用与 revoscalepy Python 创建模型

此示例演示如何在 SQL Server，使用从算法创建线性回归模型**revoscalepy**包。

**Revoscalepy**打包 Python 包含对象，转换，并为提供的算法类似于**RevoScaleR** R 语言包。 使用此库中，你可以创建计算上下文，移动之间的数据计算上下文、 转换数据，和使用受欢迎的算法，如逻辑和线性回归、 决策树，以及更多的预测模型定型。

有关详细信息，请参阅[revoscalepy 是什么？](../python/what-is-revoscalepy.md)和[Python 函数引用](https://docs.microsoft.com/r-server/python-reference/introducing-python-package-reference)

## <a name="prerequisites"></a>先决条件

> [!IMPORTANT]
> 若要在 SQL Server 中运行 Python 代码，你必须已安装 SQL Server 自 2017 年 1 CTP 2.0 或更高版本，并且必须安装和启用此功能**机器学习服务**与 Python。 其他版本的 SQL Server 不支持 Python 集成。

## <a name="run-the-sample-code"></a>运行示例代码

这段代码执行以下步骤：

1. 导入所需的库和函数
2. 创建与 SQL Server 的连接，并创建用于处理数据的数据源对象
3. 修改数据，以便它可以使用逻辑回归算法
4. 调用`rx_lin_mod`并定义用来拟合模型的公式
5. 生成一组基于原始数据集的预测
6. 创建基于预测值的摘要

使用 SQL Server 实例作为计算上下文执行所有操作。

通常情况下，远程计算上下文中调用 Python 的过程是在远程计算上下文中使用 R 工作方式相似。 作为从命令行中，或通过使用提供的 Python 集成组件包括在此版本的 Python 开发环境的 Python 脚本执行示例。 在代码中，你可以创建和使用计算上下文对象，以指示你想要执行的特定计算。

> [!NOTE]
> 请务必更改为相应的数据库和环境名称。
> 
> 有关从命令行运行此示例演示，请观看此视频： [Python 与 SQL Server 自 2017 年高级分析](https://www.youtube.com/watch?v=FcoY795jTcc)


### <a name="sample-code"></a>示例代码

```python
from revoscalepy import RxComputeContext, RxInSqlServer, RxSqlServerData
from revoscalepy import rx_lin_mod, rx_predict, rx_summary
from revoscalepy import RxOptions, rx_import

from pandas import Categorical
import os

def test_linmod_sql():
    sql_server = os.getenv('PYTEST_SQL_SERVER', '.')
    
    sql_connection_string = 'Driver=SQL Server;Server=' + sqlServer + ';Database=PyTestDb;Trusted_Connection=True;'
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

## <a name="discussion"></a>讨论

让我们查看代码并突出显示一些关键步骤。

### <a name="defining-a-data-source-and-compute-context"></a>定义数据源，并计算上下文

数据源是不同的计算上下文。 _数据源_定义在代码中使用的数据。 _计算上下文_定义才能执行的代码。

1. 创建 Python 变量，如`sql_query`和`sql_connection_string`，定义在源和你想要使用的数据。 将对这些变量传递[RxSqlServerData](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxsqlserverdata)构造函数来实现**数据源对象**名为`data_source`。
2. 通过创建计算上下文对象[RxInSqlServer](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rxinsqlserverdata)构造函数。 在此示例中，你将传递定义你将使用作为计算上下文的相同 SQL Server 实例上的数据是假定的更早版本，相同的连接字符串。 但是，数据源和计算上下文可能在不同服务器上。 生成**计算上下文对象**名为`sql_cc`。
3. 选择的主动计算上下文。 默认情况下，操作在本地运行，这意味着，如果没有指定不同的计算上下文、 将从数据源提取数据和模型调整将在你当前的 Python 环境中运行。

### <a name="changing-compute-contexts"></a>更改计算上下文

你可以在此示例中，来设置使用的单个自变量计算上下文**rx**函数。
    
`linmod = rx_lin_mod_ex("ArrDelay ~ DayOfWeek", data = data, compute_context = sql_compute_context)`

这同样适用于在调用**rxsummary**，其中重用计算上下文。

`summary = rx_summary("ArrDelay ~ DayOfWeek", data = data_source, compute_context = sql_compute_context)`

你还可以使用该函数[rx_set_computecontext](https://docs.microsoft.com/r-server/python-reference/revoscalepy/rx-set-compute-context)已定义的计算上下文之间进行切换。

### <a name="setting-the-degree-of-parallelism"></a>设置并行度

当你定义的计算上下文时，你还可以设置参数计算上下文中的数据的处理方式该控件。 这些参数与不同，具体取决于数据源类型。

对于 SQL Server 计算上下文，你可以设置批大小，或提供有关要在正在运行的任务中使用的并行度提示。

该示例已具有四个处理器的计算机上运行，因此我们将设置*num_tasks*为 4 的参数。 如果此值设置为 0 时，SQL Server 将使用默认设置，即能够尽可能情况下，在服务器的当前 MAXDOP 设置并行运行多个任务。但是，即使在处理器较多的服务器，可能会分配的任务的精确数目取决于许多其他因素，如服务器设置和运行其他作业。

## <a name="related-samples"></a>相关的示例

请参阅这些 Python 示例和高级的提示和端到端演示的教程。

+ [SQL 开发人员的数据库中 Python](sqldev-in-database-python-for-sql-developers.md)
+ [构建预测模型使用 Python 和 SQL Server](https://microsoft.github.io/sql-ml-tutorials/python/rentalprediction/)
+ [部署和使用 Python 模型](../python/publish-consume-python-code.md)
