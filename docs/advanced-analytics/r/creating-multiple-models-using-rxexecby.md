---
title: 创建多个模型使用 rxExecBy （SQL Server 机器学习） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b83abad65689e3e12310251d09199f5aa0e7c3cb
ms.sourcegitcommit: 0d6e4cafbb5d746e7d00fdacf8f3ce16f3023306
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/11/2018
ms.locfileid: "49085123"
---
# <a name="creating-multiple-models-using-rxexecby"></a>使用 rxExecBy 创建多个模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017 CTP 2.0 包括一个新的函数**rxExecBy**，支持并行处理的多个相关模型。 而不是训练一个非常大的模型基于多个类似的实体中的数据，数据科研人员可以非常快速地创建多个相关的模型，每个使用特定于单个实体的数据。

例如，假设是设备失败进行监视和捕获的许多不同类型的设备的数据。 通过使用 rxExecBy，您可以提供单个大型数据集作为输入、 指定的分层数据集，如设备类型的列，然后创建各个设备的多个模型。

此过程已被称为"愉悦 parallel"处理某种程度上繁重的数据科学家或充其量枯燥的过程，并使其快速、 简单的操作的任务，因此。

此方法的典型应用程序包括预测单个家庭智能电表、 创建单独的产品行的收入预测或创建专门针对于各银行分支机构的贷款审批的模型。

## <a name="how-rxexec-works"></a>RxExec 的工作原理

RevoScaleR 中的 rxExecBy 函数专为大规模并行处理到多个的小型数据集。

1. 你的 R 代码中，一部分调用 rxExecBy 函数并传递的无序数据的数据集。
2. 指定数据应进行分组和排序的分区。
3. 定义一个转换或建模应该应用到每个数据分区的函数
4. 执行函数时，如果您的环境支持它是并行处理数据查询。 此外，这些建模或转换任务分布在各个核心并以并行方式执行。 支持的计算上下文的三个操作包括 RxSpark 和 RxInSQLServer。
5. 返回多个结果。

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 语法和示例

**rxExecBy**采用四个输入、 一个输入正在进行分区的数据集或数据源对象上指定**密钥**列。 该函数将返回每个分区的输出。 输出的形式取决于作为参数传递的函数，例如，如果通过如 rxLinMod 的建模函数，您可以返回每个分区的数据集单独训练的模型。

### <a name="supported-functions"></a>支持的函数

建模： `rxLinMod`， `rxLogit`， `rxGlm`， `rxDtree`

评分： `rxPredict`，

转换或分析： `rxCovCor`

## <a name="example"></a>示例

下面的示例演示如何创建使用航班数据集，其中 [DayOfWeek] 列进行了分区的多个模型。 用户定义函数中， `delayFunc`，通过调用 rxExecBy 应用于每个分区。 该函数将单独的模型创建的星期一、 星期二，依此类推。

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

如果收到错误， `varsToPartition is invalid`，检查是否正确键入的键列或列的名称。 R 语言是区分大小写。

请注意，此示例中不适用于 SQL Server，并且你可以在许多情况下只需使用 SQL 对数据进行分组，这样就可以实现更好的性能。 但是，使用 rxExecBy，您可以创建并行作业从。

下面的示例说明了在 R 中，使用 SQL Server 计算上下文作为过程：

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


