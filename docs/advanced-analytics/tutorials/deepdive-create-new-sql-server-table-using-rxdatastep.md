---
title: 使用 RevoScaleR rxDataStep 创建新的 SQL Server 表
description: 有关如何在 SQL Server 上使用 R 语言创建 SQL Server 表的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b18f2bd42070746551d21ff7508e7fce58b49037
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714912"
---
# <a name="create-new-sql-server-table-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>使用 rxDataStep 创建新 SQL Server 表 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

在本课中, 您将学习如何在内存中数据帧、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上下文和本地文件之间移动数据。

> [!NOTE]
> 本课使用不同的数据集。 航空公司延迟数据集是广泛用于机器学习试验的公共数据集。 在此示例中使用的数据文件在与其他产品示例相同的目录中提供。

## <a name="load-data-from-a-local-xdf-file"></a>从本地 XDF 文件加载数据

在本教程的前半部分中, 使用**RxTextData**函数将数据从文本文件导入 R 中, 然后使用**RxDataStep**函数将数据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]移入。

本课程采用不同的方法, 并使用以[XDF 格式](https://en.wikipedia.org/wiki/Extensible_Data_Format)保存的文件中的数据。 使用 XDF 文件对数据执行一些轻型转换后, 将转换后的数据保存到新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]表中。

**什么是 XDF？**

XDF 格式是为三维数据开发的 XML 标准, 是[Machine Learning Server](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-xdf)使用的本机文件格式。 其为二进制文件格式，具有用于优化行和列的处理与分析的 R 接口。  可将其用于移动数据和存储对分析有用的数据子集。

1. 将计算上下文设置为本地工作站。 **此步骤需要 DDL 权限。**

    ```R
    rxSetComputeContext("local")
    ```
  
2. 使用 RxXdfData 函数定义新数据源对象。 若要定义 XDF 数据源, 请指定数据文件的路径。  

    您可以使用文本变量指定文件的路径。 但在这种情况下, 有一个便捷的快捷方式, 就是使用**rxGetOption**函数, 并从示例数据目录中获取文件 (airlinedemosmall.xdf. xdf)。
  
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
> 你是否注意将数据加载到 XDF 文件时不需要调用任何其他函数，并可立即对该数据调用 rxGetVarInfo？ 这是因为, XDF 是**RevoScaleR**的默认临时存储方法。 除了 XDF 文件, **rxGetVarInfo**函数现在还支持多个源类型。

## <a name="move-contents-to-sql-server"></a>将内容移动到 SQL Server

使用在本地 R 会话中创建的 XDF 数据源, 现在可以将此数据移到数据库表中, 并将*DayOfWeek*存储为值介于1到7之间的整数。

1. 定义 SQL Server 数据源对象, 指定要包含数据的表, 并连接到远程服务器。
  
    ```R
    sqlServerAirDemo <- RxSqlServerData(table = "AirDemoSmallTest", connectionString = sqlConnString)
    ```
  
2. 作为预防措施, 请包含一个步骤, 用于检查同名的表是否已存在, 如果表存在, 则删除该表。 具有相同名称的现有表禁止创建新表。
  
    ```R
    if (rxSqlServerTableExists("AirDemoSmallTest",  connectionString = sqlConnString))  rxSqlServerDropTable("AirDemoSmallTest",  connectionString = sqlConnString)
    ```
  
3. 使用**rxDataStep**将数据加载到表中。 此函数在两个已定义的数据源之间移动数据, 并且可以选择在路由时转换数据。
  
    ```R
    rxDataStep(inData = xdfAirDemo, outFile = sqlServerAirDemo,
        transforms = list( DayOfWeek = as.integer(DayOfWeek),
        rowNum = .rxStartRow : (.rxStartRow + .rxNumRows - 1) ),
        overwrite = TRUE )
    ```
  
    这是一个相当大的表, 因此请等待, 直到看到如下所示的最终状态消息:*读取的行数:200000, 处理的总行数:600000*。
     
## <a name="load-data-from-a-sql-table"></a>从 SQL 表加载数据

一旦表中存在数据, 就可以使用简单的 SQL 查询来加载数据。 

1. 创建新的 SQL Server 数据源。 输入是对刚刚创建并与数据一起加载的新表的查询。 此定义使用**RxSqlServerData**的*ColInfo*参数为*DayOfWeek*列添加因子级别。
  
    ```R
    sqlServerAirDemo2 <- RxSqlServerData(
        sqlQuery = "SELECT * FROM AirDemoSmallTest",
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",  levels = as.character(1:7))))
    ```
  
2. 再次调用**rxSummary** , 以查看查询中的数据摘要。
  
    ```R
    rxSummary(~., data = sqlServerAirDemo2)
    ```

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 rxDataStep 执行区块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)