---
title: "创建新的 SQL Server 表使用 rxDataStep （SQL 和 R 深入） |Microsoft 文档"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 98cead96-6de7-4edf-98b9-a1efb09297b9
caps.latest.revision: "19"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 5a414c590f72a1b1cfef9a3dbd8082a500592140
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-and-r-deep-dive"></a>创建新的 SQL Server 表使用 rxDataStep （SQL 和 R 深入）

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在本课程中，你学习如何内存中数据帧之间移动数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上下文和本地文件。

> [!NOTE]
> 本课程中使用不同的数据集。 航班延迟数据集是广泛用于机器学习试验的公共数据集。 此示例中使用的数据文件与其他产品示例相同的目录中可用。

## <a name="create-sql-server-table-from-local-data"></a>从本地数据创建 SQL Server 表

在本教程的第一个部分，您使用**RxTextData**函数以将数据导入从一个文本文件，R，然后使用**RxDataStep**函数将数据插入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

本课程采用不同的方法，并使用文件中的数据保存在[XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)。 在执行某些轻型转换使用 XDF 文件的数据之后, 你将保存的已转换的数据到一个新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。

**什么是 XDF？**

XDF 格式是一 XML 标准开发高维数据并通过使用本机文件格式[机器学习服务器](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 其为二进制文件格式，具有用于优化行和列的处理与分析的 R 接口。  可将其用于移动数据和存储对分析有用的数据子集。

1. 将计算上下文设置为本地工作站。 **此步骤需要 DDL 权限。**

  
    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 RxXdfData 函数定义新数据源对象。 若要定义 XDF 数据源，指定数据文件的路径。  

    你可以指定使用的文本变量的文件的路径。 但是，在这种情况下，没有方便快捷方式，就是使用**rxGetOption**函数，并从示例数据目录获取文件 (AirlineDemoSmall.xdf)。
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 对内存中数据调用 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 以查看数据集的摘要。
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**结果**

*Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)*

*Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)*

*Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday*

> [!NOTE]
> 
> 你是否注意将数据加载到 XDF 文件时不需要调用任何其他函数，并可立即对该数据调用 rxGetVarInfo？ 这是因为 XDF 是针对 RevoScaleR 的默认临时存储方法。 除了 XDF 文件**rxGetVarInfo**函数现在支持多个源类型。
  
4. 将此数据插入[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表，存储_DayOfWeek_作为值从 1 到 7 之间的整数。
  
    为此，请首先定义 SQL Server 数据源。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
5. 检查是否已存在具有相同名称的表并删除该表（如果存在）。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
6. 使用 **rxDataStep** 创建表并加载数据。 此函数将两个之间的数据已定义数据源，并可以根据需要转换数据路由。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
            transforms = list( DayOfWeek = as.integer(DayOfWeek),
            rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
            overwrite = TRUE )
    ```
  
    这是相当大型表，因此等待，直到你看到如下所示的最终状态消息：*行读取： 200000，总行处理： 600000*。
     
7. 将计算上下文重新设置为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机。

    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
8. 对新表使用简单的 SQL 查询创建新的 SQL Server 数据源。 此定义添加了因素级别*DayOfWeek*列中，使用*colInfo*参数**RxSqlServerData**。
  
    ```R
    SqlServerAirDemo <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
9. 调用**rxSummary**以查看你的查询中的数据的摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo)
    ```

## <a name="next-step"></a>下一步

[使用 rxDataStep 执行区块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)

## <a name="previous-step"></a>上一步

[使用 rxImport 将数据加载到内存中](../../advanced-analytics/tutorials/deepdive-load-data-into-memory-using-rximport.md)
