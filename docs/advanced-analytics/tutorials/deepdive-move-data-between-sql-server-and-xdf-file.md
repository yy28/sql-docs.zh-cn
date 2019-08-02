---
title: 使用 RevoScaleR 在 SQL Server 和 XDF 文件之间移动数据
description: 有关如何在 SQL Server 上使用 XDF 和 R 语言移动数据的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7eb32a6ba915328a7f6a6baccdc948f534da1a09
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715551"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>在 SQL Server 文件和 XDF 文件之间移动数据 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

在此步骤中, 学习如何使用 XDF 文件在远程和本地计算上下文之间传输数据。 如果将数据存储在 XDF 文件中, 则可以对数据执行转换。

完成后, 可以使用该文件中的数据来创建新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 函数[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)可以将转换应用于数据, 并执行数据帧和 xdf 文件之间的转换。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>从 XDF 文件创建 SQL Server 表

对于本练习, 请再次使用信用卡欺诈数据。 在此方案中，要求对加利福尼亚州、俄勒冈州和华盛顿州的用户执行一些额外分析。 为提高效率, 您决定仅将这些状态的数据存储在您的本地计算机上, 只使用变量性别、持卡人、省/市/自治区和余额。

1. 重新使用之前创建`stateAbb`的变量来确定要包含的级别, 并将其写入新的变量中。 `statesToKeep`
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **结果**
    
    CA|或|WA
    ----|----|----
    5|38|48
    
2. 使用[!INCLUDE[tsql](../../includes/tsql-md.md)]查询定义要从 SQL Server 中引入的数据。  稍后, 将此变量用作**rxImport**的*inData*参数。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    确保没有隐藏字符，如换行符或查询中的选项卡。
  
3. 接下来, 定义使用 R 中的数据时要使用的列。例如, 在较小的数据集中, 只需三个因素级别, 因为该查询只返回三个状态的数据。  `statesToKeep`应用变量以确定要包括的正确级别。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 将计算上下文设置为 "**本地**", 因为你希望在本地计算机上提供所有数据。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函数可将数据从任何支持的数据源导入到本地 XDF 文件。 如果要对数据执行多种不同的分析, 但要避免反复运行相同的查询, 则可以使用数据的本地副本。

5. 通过将之前定义为参数的变量传递给**RxSqlServerData**来创建数据源对象。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 调用**rxImport** , 将数据写入到当前工作目录`ccFraudSub.xdf`中名为的文件。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    **RxImport 函数**返回的`ccFraud.xdf` 对象是一个轻型RxXdfData数据源对象,该对象表示存储在本地`localDs`磁盘上的数据文件。
  
7. 对 XDF 文件调用 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 以验证数据架构是否相同。
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **结果**
    
    ```R
    rxGetVarInfo(data = localDS)
    Var 1: gender, Type: factor, no factor levels available
    Var 2: cardholder, Type: factor, no factor levels available
    Var 3: balance, Type: integer, Low/High: (0, 22463)
    Var 4: state, Type: factor, no factor levels available
    ```

8. 你现在可以调用各种 R 函数来分析**localDs**对象, 就像对 SQL Server 上的源数据一样。 例如, 你可能按性别汇总:
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>后续步骤

本课程将结束**RevoScaleR**和 SQL Server 的多部分教程系列。 它为您提供了大量与数据相关的概念, 并为您提供了一种基础, 可满足您自己的数据和项目需求。

若要深入了解**RevoScaleR**的知识, 可以返回到 R 教程列表, 逐步完成可能丢失的任何练习。 或者, 查看目录中的操作方法文章, 获取有关常规任务的信息。

> [!div class="nextstepaction"]
> [SQL Server 的 R 教程](sql-server-r-tutorials.md)