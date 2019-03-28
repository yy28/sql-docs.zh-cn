---
title: 创建使用 RevoScaleR RxSqlServerData-SQL Server 机器学习的 SQL Server 数据对象
description: 有关如何在 SQL Server 上使用 R 语言创建数据对象的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 45643dbcdc2876fe0794ddb731abe6334537169c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510354"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>SQL Server 数据使用 RxSqlServerData 创建对象 （SQL Server 和 RevoScaleR 教程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

第二课是数据库创建的延续： 添加表和加载数据。 如果某一 DBA 创建的数据库和登录名[第一课](deepdive-work-with-sql-server-data-using-r.md)中，可以添加表使用 RStudio 之类的 R IDE 或之类的内置工具**Rgui**。

从 R 连接到 SQL Server 并使用**RevoScaleR**函数来执行以下任务：

> [!div class="checklist"]
> * 创建定型数据和预测表
> * 从本地.csv 文件加载具有数据的表

示例数据是模拟的信用卡欺诈数据 （ccFraud 数据集），分区为定型和计分数据集。 中包括的数据文件**RevoScaleR**。

使用 R IDE 或**Rgui**才能完成这些任务。 请务必使用在此位置中找到 R 可执行文件：C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (如果使用该工具或指向 C:\Program Files\Microsoft\R Client\R_SERVER R IDE 任一 Rgui.exe)。 无[R 客户端工作站](../r/set-up-a-data-science-client.md)有了这些可执行文件被视为本教程的先决条件。

## <a name="create-the-training-data-table"></a>创建定型数据表

1. 在一个 R 变量中存储的数据库连接字符串。 以下是适用于 SQL Server 的有效 ODBC 连接字符串的两个示例： 使用 SQL 登录名的一个，一个用于 Windows 集成身份验证。 

   请确保服务器名称、 用户名和密码作为相应修改。

    **SQL 登录名**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>; Database=RevoDeepDive;Uid=<user_name>;Pwd=<password>"
    ```

    **Windows 身份验证**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>;Database=RevoDeepDive;Trusted_Connection=True"
    ```

2. 指定要创建的表的名称，并将它保存在一个 R 变量中。
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    由于服务器实例和数据库名称已指定作为连接字符串的一部分在合并两个变量时*完全限定*的新表的名称将成为*instance.database.schema.ccFraudSmall*。
  
3.  （可选） 指定*rowsPerRead*来控制在每个批次中读取的数据行数。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    虽然此参数是可选的则将其设置可能导致更高效计算。 增强的分析函数的大多数**RevoScaleR**并**MicrosoftML**处理区块中的数据。 *RowsPerRead*参数确定的每个区块中的行数。
  
    您可能需要尝试使用此设置以找到适当的平衡点。 如果值太大，数据访问可能很慢，如果没有足够内存来处理该大小的区块中的数据。 相反，在某些系统中，如果的值*rowsPerRead*太小，性能可以还会拖慢。
  
    作为一个初始值，使用定义的数据库引擎实例的默认批处理大小控制每个区块 （5,000 行） 中的行数。 将该值保存在变量*sqlRowsPerRead*。
  
4.  为新的数据源对象，定义一个变量，并将传递到以前定义的参数**RxSqlServerData**构造函数。 请注意，这只会创建数据源对象而不会填充它。 加载数据是一个单独的步骤。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>创建计分数据表

使用相同的步骤，创建保存计分数据使用相同的过程的表。

1. 创建一个新的 R 变量 sqlScoreTable，以存储用于计分的表的名称。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 将该变量作为参数提供给 RxSqlServerData 函数，以定义第二个数据源对象 sqlScoreDS。
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

由于已为 R 工作区中的变量定义的连接字符串和其他参数，则可以为新数据源表示不同的表、 视图或查询重用。

> [!NOTE]
> 该函数使用不同的参数，用于定义基于比用于基于查询的数据源的整个表的数据源。 这是因为 SQL Server 数据库引擎必须以不同的方式准备查询。 在本教程中，更高版本中，您将学习如何创建基于 SQL 查询的数据源对象。

## <a name="load-data-into-sql-tables-using-r"></a>将数据加载到使用 R 的 SQL 表

现在已创建了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，你可以使用相应的 **Rx** 函数将数据加载到这些表中。

**RevoScaleR**包包含特定于数据源类型的函数。 对于文本数据，使用[RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata)生成数据源对象。 有一些其他函数可用于通过 Hadoop 数据、ODBC 数据等创建数据源对象。

> [!NOTE]
> 本部分中，您必须具有**执行 DDL**针对数据库的权限。

### <a name="load-data-into-the-training-table"></a>将数据加载到定型表

1. 创建一个 R 变量*ccFraudCsv*，并将分配给该变量包含示例数据的 CSV 文件的文件路径。 中提供此数据集**RevoScaleR**。 "SampleDataDir"上是一个关键字**rxGetOption**函数。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    请注意，在调用**rxGetOption**，这 GET 方法与相关联[rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)中**RevoScaleR**。 使用此实用工具设置并与本地和远程计算上下文，如默认共享的目录或要在计算中使用的处理器 （核心） 数相关列表选项。
    
    此特定的调用中获取从正确的库，而不考虑在运行你的代码示例。 例如，尝试在 SQL Server 和开发计算机上运行该函数，查看路径有何不同。
  
2. 定义一个变量来存储新数据，并使用 RxTextData 函数指定文本数据源。
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    参数 colClasses 十分重要。 可使用它指示要将分配给从文本文件加载的每列数据的数据类型。 在此示例中，所有列都作为文本进行处理，除了命名列（它们作为整数进行处理）。
  
3. 此时，你可能想要暂停一段时间，并查看你的数据库中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 刷新数据库中表的列表。
  
    您可以看到，尽管 R 数据对象已在本地工作区中创建，但不创建表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 此外，没有数据加载从文本文件到 R 变量。
  
4. 调用该函数将数据插入[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)函数。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    假设连接字符串没有问题，短暂暂停之后，应看到类似下面这些的结果：
  
    *写入的总行数：10000，总时间：0.466* *读取的行数：10000，处理的总行数：10000，区块总时间：0.577 秒*
  
5. 刷新表的列表。 若要验证每个变量都具有正确的数据类型并且已成功导入，还可以右键单击表中的[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后选择**选择前 1000年行**。

### <a name="load-data-into-the-scoring-table"></a>将数据加载到计分表

1. 重复步骤以加载数据集用于评分到数据库。
  
    首先提供源文件的路径。
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. 使用 RxTextData 函数获取数据并将其保存在变量 inTextData 中。
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  调用 rxDataStep 函数以使用新架构和数据覆盖当前表。
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - inData 参数定义要使用的数据源。
  
    - outFile 参数指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中要用于保存数据的表。
  
    - 如果该表已存在并且不使用*覆盖*选项，而无需截断插入结果。
  
同样，如果连接成功，你将看到一条消息，表明完成以及将数据写入到表中所需的时间：

*写入的总行数：10000，总时间：0.384*
*读取的行数：10000，处理的总行数：10000，区块总时间：0.456 秒*

## <a name="more-about-rxdatastep"></a>有关 rxDataStep 的详细信息

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)是功能强大的函数，可以对 R 数据帧执行多个转换。 此外可以使用 rxDataStep 将数据转换为目标所需的表示形式： 在这种情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

或者，您可以指定转换的数据，通过将 R 函数的参数**rxDataStep**。 本教程中稍后提供了这些操作的示例。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)