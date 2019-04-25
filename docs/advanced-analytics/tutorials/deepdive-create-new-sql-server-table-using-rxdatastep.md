---
title: 创建使用 RevoScaleR rxDataStep-SQL Server 机器学习的新 SQL Server 表
description: 有关如何创建 SQL Server 表中的 SQL Server 上使用 R 语言的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 1fb3f83cd3bbd39e3af4936ce8dfb8f16bad82d8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641460"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>新 SQL Server 使用 rxDataStep 创建表 （SQL Server 和 RevoScaleR 教程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在本课中，了解如何在内存中数据帧、 之间移动数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上下文和本地文件。

> [!NOTE]
> 本课程中使用不同的数据集。 航班延迟数据集是广泛用于机器学习试验的公用数据集。 在此示例中使用的数据文件位于与其他产品示例相同的目录。

## <a name="load-data-from-a-local-xdf-file"></a>从本地 XDF 文件加载数据

在本教程的第一个部分，使用**RxTextData**函数将数据导入 R 中来自一个文本文件，然后使用**RxDataStep**函数将数据插入移动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

本课程中采用不同的方法，并使用文件中的数据保存在[XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)。 执行一些轻型转换使用 XDF 文件的数据之后, 您转换的数据保存到新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表。

**XDF 是什么？**

XDF 格式是为高维数据开发的 XML 标准，通过使用本机文件格式[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)。 其为二进制文件格式，具有用于优化行和列的处理与分析的 R 接口。  可将其用于移动数据和存储对分析有用的数据子集。

1. 将计算上下文设置为本地工作站。 **此步骤需要 DDL 权限。**

    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 RxXdfData 函数定义新数据源对象。 若要定义 XDF 数据源，请指定数据文件的路径。  

    可以指定使用文本变量文件的路径。 但是，在这种情况下，没有方便的快捷方式，就是使用**rxGetOption**函数，并从示例数据目录获取文件 (AirlineDemoSmall.xdf)。
  
    ```R
    xdfAirDemo <- RxXdfData(file.path(rxGetOption("sampleDataDir"),  "AirlineDemoSmall.xdf"))
    ```

3. 对内存中数据调用 [rxGetVarInfo](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxgetvarinfoxdf) 以查看数据集的摘要。
  
    ```R
    rxGetVarInfo(xdfAirDemo)
    ```

**结果**

```R
Var 1: ArrDelay, Type: integer, Low/High: (-86, 1490)
Var 2: CRSDepTime, Type: numeric, Storage: float32, Low/High: (0.0167, 23.9833)
Var 3: DayOfWeek 7 factor levels: Monday Tuesday Wednesday Thursday Friday Saturday Sunday
```

> [!NOTE]
> 
> 你是否注意将数据加载到 XDF 文件时不需要调用任何其他函数，并可立即对该数据调用 rxGetVarInfo？ 这是因为 XDF 是针对的默认临时存储方法**RevoScaleR**。 除了 XDF 文件**rxGetVarInfo**函数现在支持多个源类型。

## <a name="move-contents-to-sql-server"></a>将内容移动到 SQL Server

与在本地 R 会话中创建 XDF 数据源，您可以现在将这些数据移到数据库表中，存储*DayOfWeek*作为一个整数，其值从 1 到 7。

1. 定义 SQL Server 数据源对象，指定要包含数据和远程服务器连接的表。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 作为预防措施，包括检查是否具有相同名称的表已经存在，并且如果它存在，则删除表的步骤。 相同的名称的现有表，可防止一个新创建。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. 将数据加载到表使用**rxDataStep**。 此函数将两个数据已定义数据源，并可以根据需要转换途中的数据。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    这是相当大的表，因此等待，直到您看到与此类似的最终状态消息：*读取的行：处理 200000，总行数：600000*.
     
## <a name="load-data-from-a-sql-table"></a>从 SQL 表加载数据

后表中存在数据，可以使用简单的 SQL 查询来加载它。 

1. 创建新的 SQL Server 数据源。 输入是对新表您刚刚创建并加载数据的查询。 此定义添加了因素级别*DayOfWeek*列中，使用*colInfo*参数**RxSqlServerData**。
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. 调用**rxSummary**一次以查看你的查询中的数据的摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 rxDataStep 执行区块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)