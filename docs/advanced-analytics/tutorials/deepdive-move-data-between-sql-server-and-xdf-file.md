---
title: SQL Server 和 XDF 文件 （SQL 和 R 深入） 之间移动数据 |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6eb2ed7bdda7fab662048d7e8da692253cf9c164
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31204589"
---
# <a name="move-data-between-sql-server-and-xdf-file-sql-and-r-deep-dive"></a>SQL Server 和 XDF 文件 （SQL 和 R 深入） 之间移动数据
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在此步骤中，你了解如何使用 XDF 文件来远程和本地计算上下文之间传输数据。 将数据存储在 XDF 文件，可对数据执行转换。

完成后，你使用数据文件中创建一个新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。 该函数[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)可以对数据应用转换，并执行数据帧和.xdf 文件之间的转换。
  
## <a name="create-a-sql-server-table-from-an-xdf-file"></a>从 XDF 文件创建的 SQL Server 表

对于本练习中，你的信用卡欺诈数据再次使用。 在此方案中，要求对加利福尼亚州、俄勒冈州和华盛顿州的用户执行一些额外分析。 要更好高效，您已决定将仅这些状态的数据存储在本地计算机，和使用变量性别、 持卡人、 状态和平衡。

1. 重复使用`stateAbb`之前以标识要包括，并将它们写入一个新变量的级别创建的变量`statesToKeep`。
  
    ```R
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)
    statesToKeep
    ```
    **结果**
    
    CA|或|WA
    ----|----|----
    5|38|48
    
2. 定义你想要通过带从 SQL Server 的数据使用[!INCLUDE[tsql](../../includes/tsql-md.md)]查询。  以后，你使用此变量作为*inData*参数**rxImport**。
  
    ```R
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")
    ```
  
    确保没有隐藏字符，如换行符或查询中的选项卡。
  
3. 接下来，定义要使用。 中的数据时使用的列例如，在较小的数据集，你需要仅三个因素级别，因为查询可以返回仅三种状态的数据。  应用`statesToKeep`来标识要包括的正确级别的变量。
  
    ```R
    importColInfo <- list(
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))
            )
    ```
  
4. 将计算上下文设置为**本地**，这是因为你想在本地计算机上的所有可用的数据。
  
    ```R
    rxSetComputeContext("local")
    ```
    
    [RxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdata)函数可以将数据从任何支持的数据源到本地 XDF 文件。 当你想要进行许多不同的分析数据，但想要避免反复运行相同的查询，将方便使用数据的本地副本。

5. 通过传递作为自变量到以前定义的变量中创建数据源对象**RxSqlServerData**。
  
    ```R
    sqlServerImportDS <- RxSqlServerData(
        connectionString = sqlConnString,
        sqlQuery = importQuery,
        colInfo = importColInfo)
    ```
  
6. 调用**rxImport**若要将数据写入到名为的文件`ccFraudSub.xdf`，当前工作目录中。
  
    ```R
    localDS <- rxImport(inData = sqlServerImportDS,
        outFile = "ccFraudSub.xdf",
        overwrite = TRUE)
    ```
  
    `localDs`返回对象**rxImport**函数是轻量**RxXdfData**表示的数据源对象`ccFraud.xdf`本地存储在磁盘上的数据文件。
  
7. 对 XDF 文件调用 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 以验证数据架构是否相同。
  
    ```R
    rxGetVarInfo(data = localDS)
    ```

    **结果**
    
    *rxGetVarInfo(data = localDS)*

    *Var 1：性别，类型：因素，没有可用的因素级别*

    *Var 2：持卡人，类型：因素，没有可用的因素级别*

    *Var 3：平衡，类型：整数，低/高：（0，22463）*

    *Var 4：状态，类型：因素，没有可用的因素级别*
  
8. 现在，可以调用各种不同的 R 函数分析 `localDs` 对象，正如对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的源数据执行的操作一样。 例如，你可能按性别汇总：
  
    ```R
    rxSummary(~gender + cardholder + balance + state, data = localDS)
    ```

掌握了计算上下文的使用以及各种数据源的处理后，便可以进行一些有趣的尝试。 在下一步，也是最后课中，你创建的远程服务器运行自定义 R 函数的简单模拟。

## <a name="next-step"></a>下一步

[创建简单模拟](../../advanced-analytics/tutorials/deepdive-create-a-simple-simulation.md)

## <a name="previous-step"></a>上一步

[在本地计算上下文中分析数据](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)



