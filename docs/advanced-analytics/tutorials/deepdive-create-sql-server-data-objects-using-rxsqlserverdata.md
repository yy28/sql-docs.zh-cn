---
title: "使用 RxSqlServerData 创建 SQL Server 数据对象 | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
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
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9a1da660f019ca7665735c3d9aeb352a37214924
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata"></a>使用 RxSqlServerData 创建 SQL Server 数据对象

现在你已创建了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库并具有处理数据所需的权限，你将在 R 中创建使你可以处理数据的对象（同时在服务器和工作站上）。

## <a name="create-the-sql-server-data-objects"></a>创建 SQL Server 数据对象

在此步骤中，你将使用 R 创建并填充两个表。 这两个表包含模拟信用卡欺诈数据。 一个表用于定型模型，另一个表用于计分。

若要在远程数据库上创建表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机，你将使用**RxSqlServerData**函数中提供**RevoScaleR**包。

> [!TIP]
> 如果你正在使用 R Tools for Visual Studio，从工具栏选择“R Tools”，然后单击“Windows”以查看用于调试和查看 R 变量的选项。

### <a name="create-the-training-data-table"></a>创建训练数据表

1. 在一个 R 变量中提供数据库连接字符串。 此处提供了两个适用于 SQL Server 的有效 ODBC 连接字符串的示例：一个使用 SQL 登录名，另一个适用于 Windows 集成身份验证（推荐）。

    **使用 SQL 登录名**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **使用 Windows 身份验证**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    请务必酌情修改实例名称、数据库名称、用户名和密码。
  
2. 指定要创建的表的名称，并将它保存在一个 R 变量中。
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    由于实例和数据库名称已作为连接字符串的一部分进行指定，因此在合并两个变量时，新表的完全限定名称会成为 _instance.database.schema.ccFraudSmall_。
  
3.  实例化数据源对象之前，添加一行以指定附加参数 rowsPerRead。  rowsPerRead 参数可控制在每个批次中读取的数据行数。
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    虽然此参数是可选的，不过它对于处理内存使用率和高效计算非常重要。  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中大多数增强的分析函数处理区块中的数据并累积中间结果，并在读取所有的数据后返回最终的计算。
  
    如果此参数的值太大，则数据访问可能很慢，因为没有足够的内存来有效地处理如此大型的数据区块。  在某些系统中，如果 rowsPerRead 的值太小，则性能可能会较低。
  
    对于此演练，你将使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例定义的批处理大小控制每个区块中的行数，并将该值保存在变量 sqlRowsPerRead 中。  建议你在使用大型数据集时在系统上试用此设置。
  
4.  最后，为新的数据源对象，定义一个变量，并传递给 RxSqlServerData 构造函数之前定义的参数。 请注意，这只会创建数据源对象而不会填充它。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>创建计分数据表

你将使用相同过程创建保存计分数据的表。

1. 创建一个新的 R 变量 sqlScoreTable，以存储用于计分的表的名称。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 提供作为自变量到 RxSqlServerData 函数，以定义第二个数据源对象，该变量*sqlScoreDS*。
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

由于已在 R 工作区中将连接字符串和其他参数定义为变量，因此可方便地为不同表、视图或查询创建新数据源；只需指定不同表名即可。

在本教程后面部分中，你将学习如何基于 SQL 查询创建数据源对象。

## <a name="load-data-into-sql-tables-using-r"></a>使用 R 将数据加载到 SQL 表中

现在已创建了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，你可以使用相应的 **Rx** 函数将数据加载到这些表中。

**RevoScaleR**包包含支持多个不同的数据源的函数： 对于文本数据，你将使用 RxTextData 来生成数据源对象。 有一些其他函数可用于通过 Hadoop 数据、ODBC 数据等创建数据源对象。

> [!NOTE]
> 对于此部分，必须对数据库具有“执行 DDL”权限。

### <a name="load-data-into-the-training-table"></a>将数据加载到培训表

1. 创建了 R 变量*ccFraudCsv*，并将包含示例数据的 CSV 文件的文件路径分配给变量。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    请注意实用工具函数 rxGetOption。 此函数在 **RevoScaleR** 包中提供，可帮助设置和管理与本地和远程计算上下文相关的选项，如默认共享目录、要在计算中使用的处理器（核心）数等。此调用很有用，因为它从正确而不考虑运行你的代码库中获取这些示例。 例如，尝试在 SQL Server 和开发计算机上运行该函数，查看路径有何不同。
  
2. 定义变量来存储新数据，并使用 RxTextData 函数来指定文本数据源。
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    参数 colClasses 十分重要。 可使用它指示要将分配给从文本文件加载的每列数据的数据类型。 在此示例中，所有列都作为文本进行处理，除了命名列（它们作为整数进行处理）。
  
3. 此时，你可能想要暂停些时间，并查看你的数据库中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  刷新数据库中表的列表。
  
    你将看到，尽管 R 数据对象已在本地工作区中创建，但是表尚未在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中创建。 此外，任何数据具有已不加载从文本文件到 R 变量。
  
4. 现在，调用函数 rxDataStep 将数据插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    假设连接字符串没有问题，短暂暂停之后，应看到类似下面这些的结果：
  
      *总写入的行数： 10000，总时间： 0.466*

      *行阅读： 10000，行已处理的总数： 10000，总区块时间： 0.577 秒*
  
5. 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]刷新表的列表。 若要验证每个变量具有正确的数据类型和已成功导入，还可以右键单击中的表[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]和选择**选择前 1000年行**。

### <a name="load-data-into-the-scoring-table"></a>将数据加载到评分表

1. 你将按照相同步骤将用于计分的数据集加载到数据库中。
  
    首先提供源文件的路径。
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. 使用 RxTextData 函数来获取数据并将其保存在变量中， *inTextData*。
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  调用 rxDataStep 函数，可使用新的架构和数据覆盖当前的表。
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - inData 参数定义要使用的数据源。
  
    - outFile 参数指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中要用于保存数据的表。
  
    - 如果该表已存在并且你未使用 overwrite 选项，则结果会在无截断的情况下插入。
  
同样，如果连接成功，你将看到一条消息，表明完成以及将数据写入到表中所需的时间：

*总写入的行数： 10000，总时间： 0.384*

*行阅读： 10000，行已处理的总数： 10000，总区块时间： 0.456 秒*

## <a name="more-about-rxdatastep"></a>有关 rxDataStep 的详细信息

**RxDataStep**是一个功能强大的函数，可以执行多个转换的 R 数据框架，将数据转换为目标所需的表示。 在此例中，目标是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

通过 rxDataStep 的自变量中使用 R 函数，还可以指定转换的数据。 你将看到更高版本的这些操作的示例。

## <a name="next-step"></a>下一步

[查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>上一步

[使用 SQL Server 数据使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)


