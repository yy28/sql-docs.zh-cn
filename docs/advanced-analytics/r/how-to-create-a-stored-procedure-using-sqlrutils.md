---
title: 如何创建存储的过程，请使用 sqlrutils |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 82af827d95def976a04ac69073b58e1420cc9130
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>创建使用 sqlrutils 存储的 pProcedure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍转换 R 代码运行与 T-SQL 存储过程的步骤。 为了获得最佳的可能结果，可能需要对代码进行某种程度的修改，以确保所有输入可参数化。

## <a name="bkmk_rewrite"></a>步骤 1. 重写 R 脚本

为获得最佳结果，则应重写 R 代码作为单个函数对其进行封装。

函数所用的所有变量应内部函数，定义，或应定义为输入参数。 请参阅[示例代码](#samples)这篇文章中。

此外，因为 R 函数的输入的参数将成为输入的参数的 sql 存储过程，你必须确保你的输入和输出符合以下类型要求：

### <a name="inputs"></a>输入

输入参数中最多可有一个数据帧。

数据帧内的对象以及函数的其他输入参数必须是以下 R 数据类型之一：
- POSIXct
- numeric
- character
- integer
- 逻辑
- raw

如果输入类型不是上述类型之一，则需进行序列化并作为 *raw*传入函数。 在这种情况下，该函数还必须包括要反序列化输入的代码。

### <a name="outputs"></a>输出

该函数可输出以下项之一：

- 包含受支持数据类型的数据帧。 数据帧中所有对象必须使用受支持数据类型之一。
- 包含最多一个数据帧的命名列表。 列表的所有成员应该使用受支持数据类型之一。
- 如果函数没有返回任何结果，则为 NULL

## <a name="step-2-generate-required-objects"></a>步骤 2. 生成所需的对象

R 代码已被清除并可以作为单个函数调用后，你将使用中的函数**sqlrutils**准备的输入和输出可以传递给构造函数的实际生成的窗体中的包存储的过程。

**sqlrutils**提供定义的输入的数据架构和类型，而定义的输出数据架构和类型的函数。 它还包括可将 R 对象转换为所需的输出类型的函数。 你可能会使多个函数调用，以创建所需的对象，具体取决于你的代码使用的数据类型。

### <a name="inputs"></a>输入

如果您的函数将接收输入，对于每个输入，调用以下函数：

- `setInputData` 如果输入数据帧
- `setInputParameter` 对于所有其他输入类型

在进行每个函数调用时，将会更高版本传递的自变量作为创建 R 对象`StoredProcedure`，若要创建完整的存储的过程。

### <a name="outputs"></a>输出

**sqlrutils**转换 R 对象如还列出了所需的 SQL Server data.frame 提供多个函数。
如果函数直接输出数据帧，并未先将其包装到列表中，则可跳过此步骤。
你可以也可以跳过转换此步骤如果您的函数，则返回 NULL。

当将列表转换或从列表中，获取特定的项选择从这些函数：

- `setOutputData` 如果要从列表中获取的变量是一个数据帧
- `setOutputParameter` 所有其他成员的列表

在进行每个函数调用时，将会更高版本传递的自变量作为创建 R 对象`StoredProcedure`，若要创建完整的存储的过程。

## <a name="step-3-generate-the-stored-procedure"></a>步骤 3. 生成的存储的过程

所有的输入和输出参数准备就绪后，请调用`StoredProcedure`构造函数。

**用法**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

为了说明，假定你想要创建名为的存储的过程**sp_rsample**使用以下参数：

- 使用现有函数**foosql**。 该函数的基础 R 函数中的现有代码**foo**，但重写的函数中所述的要求符合[本节](#bkmk_rewrite)，和名为的更新的功能与**foosql**。
- 使用数据帧**queryinput**作为输入
- 作为输出数据框架 R 变量名称，将生成**sqloutput**
- 你想要为文件中创建的 T-SQL 代码`C:\Temp`文件夹，以便你可以使用运行 SQL Server Management Studio 更高版本

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> 因为文件写入文件系统，则可以省略定义数据库连接的自变量。

函数的输出是可以在 SQL Server 2016 （需要 R Services） 或 SQL Server 2017 （需要使用 R 的机器学习服务） 的实例执行的 T-SQL 存储过程。 

其他示例，请参阅的包帮助，通过调用`help(StoredProcedure)`从 R 环境。

## <a name="step-4-register-and-run-the-stored-procedure"></a>步骤 4. 注册并运行存储的过程

有两种方法，你可以运行存储的过程：

- 从任何支持连接到 SQL Server 2016 或 SQL Server 2017 实例的客户端使用 T-SQL 的
- 从 R 环境

这两种方法需要，在你想要使用存储的过程的数据库中注册该存储的过程。

### <a name="register-the-stored-procedure"></a>注册存储的过程

您可以注册存储的过程使用 R，或者你可以在 T-SQL 中运行 CREATE PROCEDURE 语句。

- 使用 T-SQL。  如果你是使用 T-SQL 更舒服，打开 SQl Server Management Studio （或可以运行 SQL DDL 命令的任何其他客户端） 和执行使用准备的代码的 CREATE PROCEDURE 语句`StoredProcedure`函数。
- 使用。当仍在 R 环境中，你可以使用`registerStoredProcedure`函数中**sqlrutils**若要向数据库中注册该存储的过程。

  例如，你无法注册该存储的过程**sp_rsample**在实例和数据库中定义*sqlConnStr*，通过进行此 R 调用：

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> 无论使用 R 或 SQL，您必须运行使用具有创建新的数据库对象的权限的帐户的语句。

### <a name="run-using-sql"></a>使用 SQL 运行

创建存储的过程后，打开与使用支持 T-SQL 的任何客户端的 SQL 数据库的连接，并将为任何所需的存储过程的参数的值传递。

### <a name="run-using-r"></a>运行使用 R

如果你想要从 R 代码，而是从 SQL Server 执行存储的过程，则需要一些额外的准备工作。 例如，如果存储的过程要求输入的值，该函数可执行，并将这些对象传递到 R 代码中的存储过程之前必须设置这些输入的参数。

调用已准备的 SQL 存储过程的整个过程是，如下所示：

1. 调用 `getInputParameters` 以获取输入参数对象的列表。
2. 定义 `$query` 或为每个输入参数设置 `$value` 。
3. 使用 `executeStoredProcedure` 从 R 开发环境执行该存储过程，传递设置的输入参数对象列表。

## <a name = "samples"></a>示例

此示例演示之前和之后版本的 R 脚本从 SQL Server 数据库中获取数据、 对数据执行某些转换并将其保存到不同的数据库。

这个简单的示例仅用于演示如何可能会重新排列 R 代码，使其更轻松地将转换为存储过程。

### <a name="before-code-preparation"></a>在代码准备之前


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

> [!NOTE]
> 
> 当你使用 ODBC 连接而不是调用*RxSqlServerData*函数，则必须打开连接使用*rxOpen*然后你才能执行数据库上的操作。


### <a name="after-code-preparation"></a>代码准备之后

在更新的版本中，第一行定义的函数名称。 从原始的 R 解决方案的所有其他代码将成为该函数的一部分。

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

> [!NOTE]
> 
> 尽管不需要显式打开 ODBC 连接作为代码的一部分，但 ODBC 连接仍需使用 **sqlrutils**。

## <a name="see-also"></a>另请参阅

[使用 sqlrutils 生成存储过程](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)


