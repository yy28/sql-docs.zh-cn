---
title: "创建新的 SQL Server 表使用 rxDataStep |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c37cb44bdf2cc30e826ced8e06d47ec64c80f1b1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="create-new-sql-server-table-using-rxdatastep"></a>使用 rxDataStep 创建新的 SQL Server 表

在本课程中，你将学习如何在内存中数据帧、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 上下文和本地文件之间移动数据。

> [!NOTE]
> 在本课程中，你将使用另一数据集。 航班延迟数据集是广泛用于机器学习试验的公共数据集。 刚开始使用 R 时，可以很方便获得此数据进行测试，因为其用于随 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 一起发布的 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]的各种产品示例。 在本例中所需的数据文件在与其他产品示例相同的目录中提供。

## <a name="create-sql-server-table-from-local-data"></a>通过本地数据创建 SQL Server 表

在本教程的第一部分，你使用了**RxTextData**函数以将数据导入从一个文本文件，R，然后使用**RxDataStep**函数将数据插入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

在本课程中，你将使用另一方法，并从以 [XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)保存的文件中获取数据。 XDF 格式是为高维数据开发的 XML 标准。 其为二进制文件格式，具有用于优化行和列的处理与分析的 R 接口。  可将其用于移动数据和存储对分析有用的数据子集。

使用 XDF 文件对数据执行一些轻型转换后，将转换的数据保存到新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。

> [!NOTE]
> 对于此步骤需要 DDL 权限。

1. 将计算上下文设置为本地工作站。
  
    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 RxXdfData 函数定义新数据源对象。 对于 XDF 数据源，只需指定数据文件的路径。  你可以指定使用的文本变量，该文件的路径，但在这种情况下，存在是方便快捷方式，因为示例数据文件 (AirlineDemoSmall.xdf) 在 rxGetOption 函数返回的目录。
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 调用 rxGetVarInfo 对内存中数据来查看数据集的摘要。
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**结果**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> 您发现你不需要调用任何其他函数以将数据载入 XDF 文件，并可以调用 rxGetVarInfo 对数据立即？ 这是因为 XDF 是针对 RevoScaleR 的默认临时存储方法。 有关 XDF 文件的详细信息，请参阅[创建 XDF](https://msdn.microsoft.com/microsoft-r/scaler-data-xdf)。
  
4. 现在，你会将此数据置于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中，从而使用 1 到 7 之间的值将 _DayOfWeek_ 存储为整数。
  
    为此，请首先定义 SQL Server 数据源。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. 检查是否已存在具有相同名称的表并删除该表（如果存在）。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. 使用 **rxDataStep** 创建表并加载数据。 此函数将两个之间的数据已定义数据源，并可以转换数据路由。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    这是一个相当大的表，因此将等到你看到最终状态消息：*读取的行数: 200000，已处理的总行数: 600000*。
     
7. 将计算上下文重新设置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机。

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. 对新表使用简单的 SQL 查询创建新的 SQL Server 数据源。 此定义使用 RxSqlServerData 的 *colInfo* 参数为 *DayOfWeek* 列添加了因素级别。
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. 调用 rxSummary 以查看你的查询中的数据的摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>下一步

[执行使用 rxDataStep 分块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>上一步

[将数据加载到内存中用 rxImport](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)


