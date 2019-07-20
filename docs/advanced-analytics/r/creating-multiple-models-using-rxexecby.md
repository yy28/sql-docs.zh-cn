---
title: 使用 rxExecBy 创建多个模型
description: 使用 RevoScaleR 库中的 rxExecBy 函数, 通过 SQL Server 中存储的计算机数据来生成多个小型模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1c51691ad55ac8aa340eb71257489bd14c0099a5
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345539"
---
# <a name="creating-multiple-models-using-rxexecby"></a>使用 rxExecBy 创建多个模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 中的**rxExecBy**函数支持对多个相关模型进行并行处理。 数据科学家可以使用特定于单个实体的数据快速创建许多相关的模型, 而不是基于多个类似实体中的数据来训练一个大型模型。 

例如, 假设要监视设备故障, 并捕获多种不同类型设备的数据。 通过使用 rxExecBy, 你可以提供单个大型数据集作为输入, 指定要对其分层数据集的列 (例如设备类型), 然后为单个设备创建多个模型。

这种用例称为["pleasingly 并行"](https://en.wikipedia.org/wiki/Embarrassingly_parallel) , 因为它会将较大的复杂问题打破为并发处理的组成部分。

此方法的典型应用包括预测单个家庭智能计量, 为单独的产品线创建收入预测, 或为单独银行分支定制的贷款审批创建模型。

## <a name="how-rxexec-works"></a>RxExec 的工作原理

RevoScaleR 中的 rxExecBy 函数旨在针对大量小数据集进行大容量并行处理。

1. 在 R 代码中调用 rxExecBy 函数, 并传递无序数据的数据集。
2. 指定用于对数据进行分组和排序的分区。
3. 定义应该应用于每个数据分区的转换或建模函数
4. 当函数执行时, 如果你的环境支持数据查询, 则会并行处理这些数据。 而且, 建模或转换任务分布在单独的内核中, 并并行执行。 支持的三个操作的计算上下文包括 RxSpark 和 RxInSQLServer。
5. 返回多个结果。

## <a name="rxexecby-syntax-and-examples"></a>rxExecBy 语法和示例

**rxExecBy**采用四个输入, 其中一个输入是可根据指定**键**列进行分区的数据集或数据源对象。 该函数返回每个分区的输出。 输出的形式取决于作为参数传递的函数。 例如, 如果传递了一个建模函数 (如 rxLinMod), 则可以为数据集的每个分区返回单独的定型模型。

### <a name="supported-functions"></a>支持的函数

建模: `rxLinMod`、 `rxLogit`、 `rxGlm`、`rxDtree`

评分: `rxPredict`,

转换或分析:`rxCovCor`

## <a name="example"></a>示例

下面的示例演示如何使用在 [DayOfWeek] 列上分区的航空公司数据集创建多个模型。 用户定义函数`delayFunc`通过调用 rxExecBy 应用于每个分区。 函数为星期一、星期二等创建单独的模型。

```sql
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

如果收到错误, `varsToPartition is invalid`请检查是否正确键入了键列的名称。 R 语言区分大小写。

此特定示例未针对 SQL Server 进行优化, 在许多情况下, 你可以使用 SQL 对数据进行分组, 从而获得更好的性能。 但是, 使用 rxExecBy 可以从 R 创建并行作业。

下面的示例使用 SQL Server 作为计算上下文, 阐释了 R 中的进程:

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


