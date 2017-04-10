---
title: "如何使用 sqlrutils 创建存储过程 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# 如何使用 sqlrutils 创建存储过程
本主题介绍了转换 R 代码以作为 T-SQL 存储过程运行的步骤。 为了获得最佳的可能结果，可能需要对代码进行某种程度的修改，以确保所有输入可参数化。

## <a name="step-1-format-your-r-script"></a>步骤 1. 设置 R 脚本的格式

1. 将所有代码包装到单个函数。

   这意味着所有用于函数的变量必须在函数内进行定义，或应定义为输入参数。 请参阅本主题中的[示例代码](#samples)。

## <a name="step-2-standardize-the-inputs-and-outputs"></a>步骤 2. 标准化输入和输出

函数的输入参数将成为 SQL 存储过程的输入参数，因此其应符合以下类型要求：
- 输入参数中最多可有一个数据帧。
- 数据帧内的对象以及函数的其他输入参数必须是以下 R 数据类型之一：
    - POSIXct
    - numeric
    - character
    - integer
    - 逻辑
    - raw

- 如果输入类型不是上述类型之一，则需进行序列化并作为 *raw* 传入函数。 在这种情况下，该函数还必须包括要反序列化输入的代码。

该函数可输出以下项之一：

- 包含受支持数据类型的数据帧。 数据帧中所有对象必须使用受支持数据类型之一。
- 包含最多一个数据帧的命名列表。 列表的所有成员应该使用受支持数据类型之一。 
- 如果函数没有返回任何结果，则为 NULL

## <a name="step-3-make-calls-to-the-sqlrutils-package-to-generate-the-stored-procedure"></a>步骤 3. 调用 sqlrutils 包，生成存储过程

清除 R 代码并将其调用为单个函数之后，可开始使用 **sqlrutils** 中函数的过程，将代码转换为存储过程。

根据参数的数据类型，使用不同的函数捕获数据并创建参数对象。

1. 如果函数采用输入参数，请针对每个参数创建以下对象之一： 
    - 如果输入参数是数据帧，请使用 `setInputData`。
    - 对于所有其他输入参数，请使用 `setInputParameter`。

2. 如果函数输出列表，请创建对象以处理列表中的所需数据，如下所示： 
    - 如果列表中的变量是数据帧，请使用 `setOutputData`。
    - 对于列表的所有其他成员，请使用 `setOutputParameter`。
    - 如果函数直接输出数据帧，并未先将其包装到列表中，则可跳过此步骤。 
    - 如果函数返回 NULL，可跳过此步骤。

3. 所有输入和输出参数准备就绪后，请调用 `StoredProcedure` 构造函数，生成包含 R 函数的存储过程。
4. 若要直接向数据库注册存储过程，可使用 `registerStoredProcedure`。

## <a name="step-4-execute-the-stored-procedure"></a>步骤 4. 执行该存储过程

1. 如果要从 R 代码而不是 SQL Server 执行存储过程，并且存储过程要求输入，则必须设置这些输入参数，然后才能执行函数： 
    - 调用 `getInputParameters` 以获取输入参数对象的列表。
    - 定义 `$query` 或为每个输入参数设置 `$value`。 

2. 使用 `executeStoredProcedure` 从 R 开发环境执行该存储过程，传递设置的输入参数对象列表。

## <a name="a-name-samplesaexamples-prepare-your-code"></a><a name = "samples"></a>示例：准备代码 

在此示例中，R 代码从数据库中读取，对数据执行某些转换，并将其保存到另一个数据库。 此简单示例仅用于演示如何重新排列 R 代码，以便为存储过程转换提供较简单的接口。

**设置格式之前**


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```
请注意，如果使用 ODBC 连接而不是调用 *RxSqlServerData* 函数，必须使用 *rxOpen* 打开连接，然后才能在数据库上执行操作。



**设置格式之后**

在重新设置格式的版本中，第一行定义函数名称。

原始 R 解决方案中的所有其他代码将成为该函数的一部分。 

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```
尽管不需要显式打开 ODBC 连接作为代码的一部分，但 ODBC 连接仍需使用 **sqlrutils**。 


## <a name="see-also"></a>另请参阅

[使用 sqlrutils 生成存储过程](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

