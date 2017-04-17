---
title: "使用 rxDataStep 创建新的 SQL Server 表（对数据科学的深入探讨）| Microsoft Docs"
ms.custom: 
ms.date: 10/03/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d88453e4f3116f0a0704c154634eb56e5180abea
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-3-2---create-new-sql-server-table-using-rxdatastep"></a>课程 3-2 - 使用 rxDataStep 创建新的 SQL Server 表
在本课程中，你将学习如何在内存中数据帧、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上下文和本地文件之间移动数据。  
  
> [!NOTE]  
> 在本课程中，你将使用另一数据集。 航班延迟数据集是广泛用于计算机学习试验的公用数据集。 刚开始使用 R 时，可以很方便获得此数据进行测试，因为其用于随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 一起发布的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的各种产品示例。 在本例中所需的数据文件在与其他产品示例相同的目录中提供。  
  
## <a name="create-sql-server-table-from-local-data"></a>通过本地数据创建 SQL Server 表  
在本教程的第一课中，你使用 RxTextData 函数将数据从文本文件导入 R 中，然后使用 RxDataStep 函数将数据移动到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中。  
  
在本课程中，你将使用另一方法，并从以 [XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)保存的文件中获取数据。 XDF 格式是为高维数据开发的 XML 标准。 其为二进制文件格式，具有用于优化行和列的处理与分析的 R 接口。  可将其用于移动数据和存储对分析有用的数据子集。
  
使用 XDF 文件对数据执行一些轻型转换后，将转换的数据保存到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。  
  
> [!NOTE]  
> 对于此步骤需要 DDL 权限。  
  
1.  将计算上下文设置为本地工作站。  
  
    ```R  
    rxSetComputeContext("local")   
    ```  
  
2.  使用 RxXdfData 函数定义新数据源对象。 对于 XDF 数据源，只需指定数据文件的路径。  可使用文本变量指定文件的路径，但在这种情况下，具有方便的快捷方式，因为示例数据文件 (AirlineDemoSmall.xdf) 处于 rxGetOption 函数返回的目录中。
  
    ```R  
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))   
    ```  
  
  
3.  对内存中数据调用 rxGetVarInfo 以查看数据集的摘要。  
  
    ```R  
    rxGetVarInfo(xdfAirDemo)    
    ```  
  
**结果**  
  
*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*   
*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*   
*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*  

> [!NOTE]
> 
> 你是否注意将数据加载到 XDF 文件时不需要调用任何其他函数，并可立即对该数据调用 rxGetVarInfo？ 这是因为 XDF 是针对 RevoScaleR 的默认临时存储方法。 有关 XDF 文件的详细信息，请参阅 [ScaleR 入门指南](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-transform#using-the-data-step-to-create-an-xdf-file-from-a-data-frame) 
  
4.  现在，你会将此数据置于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中，从而使用 1 到 7 之间的值将 _DayOfWeek_ 存储为整数。  
  
    为此，请首先定义 SQL Server 数据源。  
  
    ```R  
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)   
    ```  
  
5.  检查是否已存在具有相同名称的表并删除该表（如果存在）。  
  
    ```R  
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)    
    ```  
  
6.  使用 *rxDataStep* 创建表并加载数据。  
  
    ```R  
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,    
            transforms = list( DayOfWeek = as.integer(DayOfWeek),   
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),   
            overwrite = TRUE )    
    ```
  
    这是一个相当大的表，因此将等到你看到最终状态消息：*读取的行数: 200000，已处理的总行数: 600000*。
     
7.  将计算上下文重新设置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机。  
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
  
8.  对新表使用简单的 SQL 查询创建新的 SQL Server 数据源。 此定义使用 RxSqlServerData 的 *colInfo* 参数为 *DayOfWeek* 列添加了因素级别。  
  
    ```R    
    SqlServerAirDemo <- RxSqlServerData(  
        sqlQuery = "SELECT * FROM AirDemoSmallTest",      
        connectionString = sqlConnString,   
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))    
    ```  
  
9. 在查询中调用 rxSummary 以查看数据的摘要。  
  
    ```R  
    rxSummary(~., data = sqlServerAirDemo)   
    ```  
  
## <a name="next-step"></a>下一步  
[使用 rxDataStep 执行区块分析（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-3-3-perform-chunking-analysis-using-rxdatastep.md)  
  
## <a name="previous-step"></a>上一步  
[使用 rxImport 将数据加载到内存中（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-3-1-load-data-into-memory-using-rximport.md)  
  
## <a name="see-also"></a>另请参阅  
[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  


