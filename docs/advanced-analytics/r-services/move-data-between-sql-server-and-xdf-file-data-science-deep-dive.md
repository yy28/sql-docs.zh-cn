---
title: "在 SQL Server 和 XDF 文件之间移动数据（对数据科学的深入探讨） | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 40887cb3-ffbb-4769-9f54-c006d7f4798c
caps.latest.revision: 17
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 在 SQL Server 和 XDF 文件之间移动数据（对数据科学的深入探讨）
在本地计算上下文中工作时，用户对本地数据文件和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库（定义为 RxSqlServerData 数据源）都具有访问权限。  
  
本部分将介绍如何获取数据并将其存储到本地计算机上的文件中，以便对数据执行转换。 完成后，通过使用 rxDataStep，用文件中的数据创建一个新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表。  
  
## 从 XDF 文件创建一个 SQL Server 表  

rxImport 函数允许将数据从任何受支持的数据源导入到本地 XDF 文件。 如果想要对存储在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的数据进行多种不同的分析，并且避免反复运行相同的查询，使用本地文件会非常方便。  
  
在本练习中，会再次使用信用卡欺诈数据。 在此方案中，要求对加利福尼亚州、俄勒冈州和华盛顿州的用户执行一些额外分析。 为了提高效率，决定在本地计算机上只存储这些州的数据并只处理 gender、ardholder、state 和 balance 这几个变量。  
  
1.  再次使用之前创建的 stateAbb 向量确定要包括的级别，然后将新变量 statesToKeep 打印到控制台。  
  
    ```  
    statesToKeep <- sapply(c("CA", "OR", "WA"), grep, stateAbb)   
  
    statesToKeep  
  
    ```  
 **结果**
CA |  或  | WA 
-- | -- | --
 5 |  38  | 48 
  
2.  现在，你将使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 查询定义想要从 SQL Server 带来的数据。  稍后，此变量将用作 rxImport 的 inData 参数。  
  
    ```R  
    importQuery <- paste("SELECT gender,cardholder,balance,state FROM",  sqlFraudTable,  "WHERE (state = 5 OR state = 38 OR state = 48)")  
  
    ```  
  
    确保没有隐藏字符，如换行符或查询中的选项卡。  
  
3.  接下来，你将定义在处理 R 中的数据时要使用的列。  
  例如，在较小的数据集中，只需三个因素级别，因为该查询只返回三个州的数据。  可以再次使用 statesToKeep 变量确定要包括的正确级别。  
  
    ```R  
    importColInfo <- list(   
        gender = list( type = "factor",  levels = c("1", "2"), newLevels = c("Male", "Female")),       
        cardholder = list(  type = "factor",  levels = c("1", "2"), newLevels = c("Principal", "Secondary")),     
        state = list(   type = "factor",  levels = as.character(statesToKeep), newLevels = names(statesToKeep))   
            )  
  
    ```  
  
4.  将计算上下文设置为**本地**，因为需在本地计算机上使用所有数据。  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
5.  通过将之前定义为参数的所有变量传递给 RxSqlServerData，创建数据源对象。  
  
    ```R  
    sqlServerImportDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        sqlQuery = importQuery,   
        colInfo = importColInfo)  
  
    ```  
  
6.  然后，调用 rxImport，将数据保存在名为 `ccFraudSub.xdf` 的文件中的当前工作目录中。  
  
    ```R  
    localDS <- rxImport(inData = sqlServerImportDS,   
        outFile = "ccFraudSub.xdf",    
        overwrite = TRUE)  
  
    ```  
  
    rxImport 函数返回的 localDs 对象是一个表示存储在本地磁盘上的 ccFraud.xdf 数据文件的轻量 RxXdfData 数据源对象。  
  
7.  对 XDF 文件调用 rxGetVarInfo 以验证数据架构是否相同。  
  
    ```R  
    rxGetVarInfo(data = localDS)   
    ```  
    **结果**
    
    *rxGetVarInfo(data = localDS)*    
    *Var 1：性别，类型：因素，没有可用的因素级别*    
    *Var 2：持卡人，类型：因素，没有可用的因素级别*    
    *Var 3：平衡，类型：整数，低/高：（0，22463）*    
    *Var 4：状态，类型：因素，没有可用的因素级别*
  
8.  现在，可以调用各种不同的 R 函数分析 localDs 对象，正如对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上的源数据执行的操作一样。 例如：  
  
    ```R  
    rxSummary(~gender + cardholder + balance + state, data = localDS)    
    ```  
  
掌握了计算上下文的使用以及各种数据源的处理后，便可以进行一些有趣的尝试。  
  
在下一课和最后一课中，将使用自定义 R 函数创建简单的模拟并在远程服务器上运行它。  
  
## 下一步  
[第 5 课：创建简单模拟（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-5-create-a-simple-simulation-data-science-deep-dive.md)  
  
## 上一步  
[第 4 课：在本地计算上下文中分析数据（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## 另请参阅  
[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
