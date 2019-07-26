---
title: 使用 RevoScaleR RxSqlServerData 创建 SQL Server 数据对象
description: 有关如何在 SQL Server 上使用 R 语言创建数据对象的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 423a90fe66749a3192c6f03c0efee314b4ceef37
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469760"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>使用 RxSqlServerData 创建 SQL Server 数据对象 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

第二课是创建数据库的任务: 添加表和加载数据。 如果 DBA 在[第一课](deepdive-work-with-sql-server-data-using-r.md)中创建了数据库和登录名, 则可以使用 R IDE (如 RStudio) 或内置工具 (如**rgui.exe**) 来添加表。

在 R 中, 连接到 SQL Server 并使用**RevoScaleR**函数执行以下任务:

> [!div class="checklist"]
> * 创建用于定型数据和预测的表
> * 使用本地 .csv 文件中的数据加载表

示例数据是模拟的信用卡欺诈数据 (Ccfraud.xdf 数据集), 分区到定型和计分数据集。 数据文件包含在**RevoScaleR**中。

使用 R IDE 或**rgui.exe**来完成这些花。 请确保使用在此位置找到的 R 可执行文件:C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (如果你使用的是该工具, 则为 Rgui.exe, 或者是指向 C:\Program Files\Microsoft\R Client\R_SERVER 的 R IDE)。 具有这些可执行文件的[R 客户端工作站](../r/set-up-a-data-science-client.md)被视为本教程的先决条件。

## <a name="create-the-training-data-table"></a>创建定型数据表

1. 将数据库连接字符串存储在 R 变量中。 下面是 SQL Server 的有效 ODBC 连接字符串的两个示例: 一个使用 SQL 登录名, 另一个用于 Windows 集成身份验证。 

   请确保根据需要修改服务器名称、用户名和密码。

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
  
    由于已将服务器实例和数据库名称指定为连接字符串的一部分, 因此当你组合这两个变量时, 新表的*完全限定*名称将成为*ccFraudSmall*。
  
3.  (可选) 指定*rowsPerRead*以控制每个批次中读取的数据行数。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    虽然此参数是可选的, 但设置它可以使计算效率更高。 **RevoScaleR**和**MicrosoftML**中的大多数增强的分析函数都在块区中处理数据。 *RowsPerRead*参数确定每个区块中的行数。
  
    你可能需要尝试此设置来找出适当的平衡。 如果值太大, 则如果内存不足, 无法处理该大小块区中的数据, 则数据访问可能会很慢。 相反, 在某些系统上, 如果*rowsPerRead*的值太小, 则性能也会降低。
  
    作为初始值, 请使用数据库引擎实例定义的默认批处理进程大小来控制每个区块中的行数 (5000 行)。 将该值保存在变量*sqlRowsPerRead*中。
  
4.  为新数据源对象定义一个变量, 并将以前定义的参数传递给**RxSqlServerData**构造函数。 请注意，这只会创建数据源对象而不会填充它。 加载数据是一个单独的步骤。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>创建计分数据表

使用相同的步骤, 使用同一过程创建保存计分数据的表。

1. 创建一个新的 R 变量 sqlScoreTable，以存储用于计分的表的名称。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 将该变量作为参数提供给 RxSqlServerData 函数，以定义第二个数据源对象 sqlScoreDS。
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

由于已在 R 工作区中将连接字符串和其他参数定义为变量, 因此可将其用于表示不同的表、视图或查询的新数据源。

> [!NOTE]
> 函数根据查询使用不同的参数来定义基于整个表的数据源。 这是因为 SQL Server 数据库引擎必须以不同的方式准备查询。 稍后在本教程中, 将了解如何创建基于 SQL 查询的数据源对象。

## <a name="load-data-into-sql-tables-using-r"></a>使用 R 将数据加载到 SQL 表中

现在已创建了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，你可以使用相应的 **Rx** 函数将数据加载到这些表中。

**RevoScaleR**包包含特定于数据源类型的函数。 对于文本数据, 请使用[RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata)生成数据源对象。 有一些其他函数可用于通过 Hadoop 数据、ODBC 数据等创建数据源对象。

> [!NOTE]
> 对于此部分, 您必须拥有对数据库的**EXECUTE DDL**权限。

### <a name="load-data-into-the-training-table"></a>将数据加载到定型表中

1. 创建 R 变量*ccFraudCsv*, 并将包含示例数据的 CSV 文件的文件路径分配给该变量。 此数据集在**RevoScaleR**中提供。 "SampleDataDir" 是**rxGetOption**函数的关键字。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    请注意对**rxGetOption**的调用, 这是与**RevoScaleR**中的[rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)关联的 GET 方法。 使用此实用程序可以设置和列出与本地和远程计算上下文相关的选项, 如默认共享目录或要在计算中使用的处理器 (核心) 数。
    
    此特定调用从正确的库中获取示例, 而不考虑您运行代码的位置。 例如，尝试在 SQL Server 和开发计算机上运行该函数，查看路径有何不同。
  
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
  
3. 此时, 你可能需要暂停片刻, 并在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]查看数据库。 刷新数据库中表的列表。
  
    你可以看到, 尽管已在本地工作区中创建 R 数据对象, 但尚未在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中创建这些表。 此外, 未将数据从文本文件加载到 R 变量中。
  
4. 通过调用函数[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)函数插入数据。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    假设连接字符串没有问题，短暂暂停之后，应看到类似下面这些的结果：
  
    *写入的总行数:10000, 总时间:* 0.466*行读取:10000, 处理的总行数:10000, 总区块时间:0.577 秒*
  
5. 刷新表的列表。 若要确认每个变量都具有正确的数据类型并且已成功导入, 还可以在中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]右键单击该表, 然后选择 "**选择前1000行**"。

### <a name="load-data-into-the-scoring-table"></a>将数据加载到计分表中

1. 重复上述步骤, 将用于计分的数据集加载到数据库中。
  
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
  
    - 如果表已存在并且您不使用 "*覆盖*" 选项, 则会在不截断的情况下插入结果。
  
同样，如果连接成功，你将看到一条消息，表明完成以及将数据写入到表中所需的时间：

*写入的总行数:10000, 总时间:0.384*
行读取 *:10000, 处理的总行数:10000, 总区块时间:0.456 秒*

## <a name="more-about-rxdatastep"></a>有关 rxDataStep 的详细信息

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)是一个功能强大的函数, 可以对 R 数据帧执行多个转换。 还可以使用 rxDataStep 将数据转换为目标所需的表示形式: 在本例中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为。

还可以通过在**rxDataStep**的参数中使用 R 函数, 来指定对数据的转换。 本教程稍后会提供这些操作的示例。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)