---
title: 如何创建存储的过程，请使用 sqlrutils-SQL Server 机器学习服务
description: 在 SQL Server 中使用 sqlrutils R 包捆绑到一个函数可以作为参数传递给存储过程的 R 语言代码。
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 014fb8344a0b2cf93dc7f375fffc717663f53a46
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58509884"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>创建使用 sqlrutils 存储的 pProcedure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍了转换 R 代码以作为 T-SQL 存储过程运行的步骤。 为了获得最佳的可能结果，可能需要对代码进行某种程度的修改，以确保所有输入可参数化。

## <a name="bkmk_rewrite"></a>步骤 1. 重写 R 脚本

为获得最佳结果，则应重写 R 代码以将其封装作为单个函数。

该函数使用的所有变量应在函数内定义，或应定义为输入参数。 请参阅[示例代码](#samples)这篇文章中。

此外，由于 R 函数的输入的参数将成为输入的参数的 sql 存储过程，必须确保输入和输出符合以下类型要求：

### <a name="inputs"></a>输入

输入参数中最多可有一个数据帧。

数据帧内的对象以及函数的其他输入参数必须是以下 R 数据类型之一：
- POSIXct
- NUMERIC
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

在 R 代码已清除，并可作为单个函数调用后，将使用中的函数**sqlrutils**包来准备的输入和输出中可以传递给构造函数下实际生成的窗体存储的过程。

**sqlrutils**提供函数来定义输入的数据架构和类型，并定义输出数据架构和类型。 它还可以将 R 对象转换为所需的输出类型的函数。 您可能会进行多个函数调用以创建所需的对象，具体取决于你的代码使用的数据类型。

### <a name="inputs"></a>输入

如果函数采用输入，为每个输入，调用以下函数：

- `setInputData` 如果输入是数据帧
- `setInputParameter` 对于所有其他输入类型

R 对象时进行调用的每个函数，创建，你将更高版本作为参数传递到`StoredProcedure`，以创建完整的存储的过程。

### <a name="outputs"></a>输出

**sqlrutils**转换 R 对象等所需的 SQL Server data.frame 还列出了为提供多个功能。
如果函数直接输出数据帧，并未先将其包装到列表中，则可跳过此步骤。
您可以还如果跳过转换此步骤中函数返回 NULL。

当转换列表或获取特定的项从列表中选择这些函数：

- `setOutputData` 如果要从列表中获取的变量是数据帧
- `setOutputParameter` 所有其他成员的列表

R 对象时进行调用的每个函数，创建，你将更高版本作为参数传递到`StoredProcedure`，以创建完整的存储的过程。

## <a name="step-3-generate-the-stored-procedure"></a>步骤 3. 生成的存储的过程

所有输入和输出参数准备就绪后，请调用`StoredProcedure`构造函数。

**Usage**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

为了说明，假定你想要创建一个名为的存储的过程**sp_rsample**使用以下参数：

- 使用现有的函数**foosql**。 函数基于 R 函数中的现有代码**foo**，重写要符合的要求中所述的函数，但[本节](#bkmk_rewrite)，并命名为作为更新的函数**foosql**。
- 使用数据帧**queryinput**作为输入
- 生成作为输出数据框架的 R 变量名称， **sqloutput**
- 你想要为文件中创建的 T-SQL 代码`C:\Temp`文件夹中，以便可以运行更高版本使用 SQL Server Management Studio

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> 因为该文件将写入文件系统，则可以省略参数，定义数据库连接。

该函数的输出是可以在 SQL Server 2016 （需要 R Services） 或 SQL Server 2017 （需要使用 R 的机器学习服务） 的实例上执行的 T-SQL 存储过程。 

其他示例，请参阅包的帮助下，通过调用`help(StoredProcedure)`从 R 环境。

## <a name="step-4-register-and-run-the-stored-procedure"></a>步骤 4. 注册并运行存储的过程

有两种方法可以运行存储的过程：

- 使用 T-SQL、 从任何客户端支持连接到 SQL Server 2016 或 SQL Server 2017 实例
- 从 R 环境

这两种方法需要存储的过程想要使用存储的过程在数据库中注册。

### <a name="register-the-stored-procedure"></a>注册存储的过程

你可以注册存储的过程使用 R，或者您可以在 T-SQL 中运行 CREATE PROCEDURE 语句。

- 使用 T-SQL。  如果你是更加熟悉 T-SQL，打开 SQl Server Management Studio （或可以运行 SQL DDL 命令的任何其他客户端），然后执行 CREATE PROCEDURE 语句使用准备的代码`StoredProcedure`函数。
- 使用。虽然仍在你的 R 环境中，可以使用`registerStoredProcedure`函数，在**sqlrutils**若要向数据库注册存储的过程。

  例如，无法注册存储的过程**sp_rsample**中的实例和数据库中定义*sqlConnStr*，可以执行此 R 调用：

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> 无论使用 R 或 SQL，您必须运行使用的帐户有权创建新的数据库对象的语句。

### <a name="run-using-sql"></a>使用 SQL 运行

创建此存储的过程后，打开与使用任何客户端支持 T-SQL 的 SQL 数据库的连接，并传递所需的存储过程的任何参数的值。

### <a name="run-using-r"></a>运行使用 R

如果你想要从 R 代码，而不是从 SQL Server 执行存储的过程，则需要一些额外的准备工作。 例如，如果存储的过程需要输入的值，则必须设置这些输入的参数之前该函数可执行，然后将这些对象传递给 R 代码中的存储过程。

调用已准备的 SQL 存储过程的整个过程是按如下所示：

1. 调用 `getInputParameters` 以获取输入参数对象的列表。
2. 定义 `$query` 或为每个输入参数设置 `$value` 。
3. 使用 `executeStoredProcedure` 从 R 开发环境执行该存储过程，传递设置的输入参数对象列表。

## <a name = "samples"></a>示例

此示例显示了之前和之后版本的 R 脚本，以从 SQL Server 数据库获取数据、 对数据执行某些转换并将其保存到不同的数据库。

这个简单的示例仅用于演示如何重新排列 R 代码以使其更轻松地将转换为存储过程。

### <a name="before-code-preparation"></a>之前代码准备


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
> 当使用 ODBC 连接而不是调用*RxSqlServerData*函数，则必须打开连接使用*rxOpen*可以执行对数据库的操作之前。


### <a name="after-code-preparation"></a>代码准备后

在更新后的版本中，第一行定义的函数名称。 从原始 R 解决方案的所有其他代码将成为该函数的一部分。

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

## <a name="see-also"></a>请参阅

[sqlrutils (SQL)](ref-r-sqlrutils.md)


