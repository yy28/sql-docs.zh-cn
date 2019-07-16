---
title: SQL Server 和 XDF 文件使用 RevoScaleR 的 SQL Server 机器学习之间移动数据
description: 如何移动数据的 SQL Server 上使用 XDF 和 R 语言的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: f5800f315ee09328908b612c18faf6c77a7ac13c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962215"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-server-and-revoscaler-tutorial"></a>SQL Server 和 XDF 文件 （SQL Server 和 RevoScaleR 教程） 之间移动数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在此步骤中，了解如何使用 XDF 文件远程和本地计算上下文之间传输数据。 在 XDF 文件中存储数据，可对数据执行转换。

完成后，您使用数据文件中创建一个新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 该函数[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)可以对数据应用转换，并执行数据帧和.xdf 文件之间的转换。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>从 XDF 文件创建 SQL Server 表

对于此练习，你的信用卡欺诈数据再次使用。 在此方案中，要求对加利福尼亚州、俄勒冈州和华盛顿州的用户执行一些额外分析。 使其更加高效，您决定仅这些状态数据存储在本地计算机上并使用变量性别、 持卡人、 状态和平衡。

1. 重用`stateAbb`变量之前确定要包括，并将其写入到一个新的变量的级别创建`statesToKeep`。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **结果**
    
    CA|或|WA
    ----|----|----
    5|38|48
    
2. 定义你想要通过从 SQL Server 自带的数据使用[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。  更高版本使用此变量，作为*inData*参数**rxImport**。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    确保没有隐藏字符，如换行符或查询中的选项卡。
  
3. 接下来，定义要使用在 R 中的数据时使用的列例如，在较小的数据集，您需要仅三个因素级别，因为查询将返回只有三个州的数据。  将应用`statesToKeep`变量确定要包括的正确级别。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 将计算上下文设置为**本地**，因为你想在本地计算机上所有可用的数据。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函数导入的数据的任何受支持的数据源到本地 XDF 文件。 如果想要执行许多不同的分析数据，但想要避免反复运行相同的查询，使用数据的本地副本很方便。

5. 通过传递作为自变量以前定义的变量创建数据源对象**RxSqlServerData**。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 调用**rxImport**将数据写入到名为的文件`ccFraudSub.xdf`，当前工作目录中。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    `localDs`返回的对象**rxImport**函数是轻量**RxXdfData**数据源对象表示`ccFraud.xdf`数据文件存储在本地磁盘上。
  
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

8. 现在，可以调用各种 R 函数分析**localDs**对象，就像与 SQL Server 上的源数据。 例如，您可能按性别进行汇总：
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

## <a name="next-steps"></a>后续步骤

本课程中最后上多个部分组成的系列教程**RevoScaleR**和 SQL Server。 它介绍了许多相关的数据和计算的概念，为你提供一个基础来推动您自己的数据和项目要求。

进行深入的了解**RevoScaleR**，可以返回到要单步执行您可能已经遗漏了任何练习的 R 教程列表。 或者，查看表中的常规任务的信息的目录的操作方法文章。

> [!div class="nextstepaction"]
> [SQL Server 的 R 教程](sql-server-r-tutorials.md)