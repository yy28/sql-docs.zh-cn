---
title: "创建多个模型使用 rxExecBy |Microsoft 文档"
ms.custom: 
ms.date: 04/18/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 685833317453c1ed5765385a73ff892a85989c2c
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="creating-multiple-models-using-rxexecby"></a>创建使用 rxExecBy 的多个模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 自 2017 年 1 CTP 2.0 包括一个新函数**rxExecBy**，支持多个相关模型的并行处理。 而不是训练一个非常大的模型基于从多个类似的实体的数据，数据科研人员可以非常快速地创建多个相关的模型，每个使用特定于单个实体的数据。

例如，假设您是监视设备失败，并捕获许多不同类型的设备的数据。 通过使用 rxExecBy，你可以提供单个大型数据集作为输入，指定分层数据集，如设备类型，所依据的列，然后创建单独的设备的多个模型模型。

此过程已被称为"pleasingly parallel"处理，因为它采用某种程度上繁重的数据科学家，或在最好的单调乏味，并使其成为快速、 简单的操作的任务。

此方法的典型应用程序包括为单个家庭智能米预测、 创建为单独的产品行、 收入投影或创建于单个银行分支机构的贷款审批的模型。

## <a name="how-rxexec-works"></a>RxExec 的工作原理

中 RevoScaleR 的 rxExecBy 函数旨在为大量并行处理通过大量的小型数据集。

1. 作为一部分的 R 代码，调用 rxExecBy 函数并传递未排序的数据的数据集。
2. 指定的分区的数据应分组和排序。
3. 定义转换或建模应该应用到每个数据分区的函数
4. 该函数执行时，数据查询处理并行，如果你的环境支持它。 此外，建模或转换任务将分布在各个内核和并行执行。 支持的计算上下文为三个操作包括 RxSpark 和 RxInSQLServer。
5. 返回多个结果。

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 语法和示例

**rxExecBy**采用四个输入，输入正在进行分区的数据集或数据源对象之一上指定**密钥**列。 该函数返回每个分区的输出。 形式的输出取决于作为参数传递的函数、、 例如，如果您传入如 rxLinMod 建模函数，你可以返回数据集的每个分区单独训练的模型。

### <a name="supported-functions"></a>支持的函数

建模： `rxLinMod`， `rxLogit`， `rxGlm`，`rxDtree`

评分： `rxPredict`，

转换或进行分析：`rxCovCor`

## <a name="example"></a>示例

下面的示例演示如何创建使用航班数据集，分区在 [DayOfWeek] 列的多个模型。 用户定义函数中， `delayFunc`，通过调用 rxExecBy 应用于每个分区。 该函数将单独的模型创建针对星期一、 星期二，依次类推。

```SQL
EXEC sp_execute_external_script
@language = N'R'
, @script = N'
delayFunc <- function(key, data, params) { 
    df <- rxImport(inData = airlineData) 
    rxLinMod(ArrDelay ~ CRSDepTime, data = df) 
} 
OutputDataSet <- rxExecBy(airlineData, c("DayOfWeek"), delayFunc)
'
, @input_data_1 = N'select ArrDelay, DayOfWeek, CRSDepTime from AirlineDemoSmall]'
, @input_data_1_name = N'airlineData'

```

如果你将收到错误， `varsToPartition is invalid`，检查是否正确键入的键列或列的名称。 R 语言是区分大小写。

请注意，此示例不会优化对于 SQL Server，并且你可以在许多情况下通过使用 SQL 对数据进行分组实现更好的性能。 但是，使用 rxExecBy，你可以创建并行作业从。

下面的示例阐释了 R，使用 SQL Server 作为计算上下文中的过程：

```R
sqlServerConnString <- "SERVER=hostname;DATABASE=TestDB;UID=DBUser;PWD=Password;"
inTable <- paste("airlinedemosmall")
sqlServerDataDS <- RxSqlServerData(table = inTable, connectionString = sqlServerConnString)

# user function
".Count" <- function(keys, data, params)
{
  myDF <- rxImport(inData = data)
  return (nrow(myDF))
}

# Set SQL Server compute context with level of parallelism = 2
sqlServerCC <- RxInSqlServer(connectionString = sqlServerConnString, numTasks = 4)
rxSetComputeContext(sqlServerCC)

# Execute rxExecBy in SQL Server compute context
sqlServerCCResults <- rxExecBy(inData = sqlServerDataDS, keys = c("DayOfWeek"), func = .Count)
```


