---
title: 创建 SQL Server 数据对象使用 RxSqlServerData （SQL 和 R 深入） |Microsoft 文档
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e15c3e7c13c1be4f524c25bb1cec6da3c8e20c7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203459"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-and-r-deep-dive"></a>创建使用 RxSqlServerData （SQL 和 R 深入） 的 SQL Server 数据对象
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

到目前为止已创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库中，并且具有足够的权限来处理的数据。 在此步骤中，你将创建可以处理的数据的 R 中的一些对象。

## <a name="create-the-sql-server-data-objects"></a>创建 SQL Server 数据对象

在此步骤中，使用函数从**RevoScaleR**包创建并填充两个表。 一个表用于定型模型，另一个表用于计分。 这两个表包含模拟信用卡欺诈数据。

若要在远程数据库上创建表[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机，请调用**RxSqlServerData**函数。

> [!TIP]
> 如果你正在使用 R Tools for Visual Studio，从工具栏选择“R Tools”，然后单击“Windows”以查看用于调试和查看 R 变量的选项。

### <a name="create-the-training-data-table"></a>创建训练数据表

1. 将数据库连接字符串保存在 R 变量中。 下面是有效的 SQL Server 的 ODBC 连接字符串的两个示例： 使用 SQL 登录名的一个，一个用于 Windows 集成身份验证。

    **SQL 登录名**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Windows 身份验证**
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
  
    虽然此参数是可选的，不过它对于处理内存使用率和高效计算非常重要。  中的增强分析函数的大多数[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]处理小区块中的数据和存储返回最终计算所有数据的已读取的中间结果。
  
    如果此参数的值太大，则数据访问可能很慢，因为没有足够的内存来有效地处理如此大型的数据区块。  在某些系统中，如果 rowsPerRead 的值太小，则性能可能会较低。 因此，我们建议要通过试验使用此设置你的系统上时你正在使用大型数据集。
  
    对于本演练中，使用所定义的默认批处理过程大小[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例来控制在每个块区中的行数。 将该值保存在变量`sqlRowsPerRead`。
  
4.  最后，为新的数据源对象，定义一个变量，并传递给 RxSqlServerData 构造函数之前定义的参数。 请注意，这只会创建数据源对象而不会填充它。
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>创建计分数据表

使用相同的步骤，创建包含使用相同的过程的评分的数据的表。

1. 创建一个新的 R 变量 sqlScoreTable，以存储用于计分的表的名称。
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. 提供作为自变量到 RxSqlServerData 函数，以定义第二个数据源对象，该变量*sqlScoreDS*。
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

由于你已定义的连接字符串和其他参数作为 R 工作区中的变量，它很容易创建不同的表、 视图或查询的新数据源。

> [!NOTE]
> 该函数使用不同的自变量，用于定义整个表比基于查询的数据源所基于的数据源。 这是因为 SQL Server 数据库引擎必须以不同的方式准备查询。 在本教程中，更高版本中，您将学习如何创建基于 SQL 查询的数据源对象。

## <a name="load-data-into-sql-tables-using-r"></a>将数据加载到使用 R 的 SQL 表

现在已创建了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表，你可以使用相应的 **Rx** 函数将数据加载到这些表中。

**RevoScaleR**包包含支持多个不同的数据源的函数： 对于文本数据，使用[RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata)生成数据源对象。 有一些其他函数可用于通过 Hadoop 数据、ODBC 数据等创建数据源对象。

> [!NOTE]
> 对于本部分中，必须具有**执行 DDL**数据库的权限。

### <a name="load-data-into-the-training-table"></a>将数据加载到培训表

1. 创建了 R 变量*ccFraudCsv*，并将包含示例数据的 CSV 文件的文件路径分配给变量。
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    请注意调用**rxGetOption**，这 GET 方法与关联[rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions)中**RevoScaleR**。 此实用程序用于设置和列表选项与本地和远程计算上下文，如默认的共享的目录或要在计算中使用的处理器 （内核） 数。
    
    此特定调用从正确库，无论运行你的代码中获取这些示例。 例如，尝试在 SQL Server 和开发计算机上运行该函数，查看路径有何不同。
  
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
  
3. 此时，你可能想要暂停些时间，并查看你的数据库中[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  刷新数据库中表的列表。
  
    你可以看到，尽管已在本地工作区中创建 R 数据对象，这些表尚未创建中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。 此外，任何数据具有已不加载从文本文件到 R 变量。
  
4. 现在，调用函数 [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) 将数据插入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 表中。
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    假设连接字符串没有问题，短暂暂停之后，应看到类似下面这些的结果：
  
      *总写入的行数： 10000，总时间： 0.466*

      *行阅读： 10000，行已处理的总数： 10000，总区块时间： 0.577 秒*
  
5. 使用 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]刷新表的列表。 若要验证每个变量具有正确的数据类型和已成功导入，还可以右键单击中的表[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]和选择**选择前 1000年行**。

### <a name="load-data-into-the-scoring-table"></a>将数据加载到评分表

1. 重复步骤要加载数据集用于评分到数据库。
  
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
  
    - 如果该表已存在并且不使用*覆盖*选项，而不发生截断插入结果。
  
同样，如果连接成功，你将看到一条消息，表明完成以及将数据写入到表中所需的时间：

*总写入的行数： 10000，总时间： 0.384*

*行阅读： 10000，行已处理的总数： 10000，总区块时间： 0.456 秒*

## <a name="more-about-rxdatastep"></a>有关 rxDataStep 的详细信息

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep)是功能强大的函数，可以在 R 数据框架上执行多个转换。 此外可以使用 rxDataStep 将数据转换为所需的目标表示形式： 在这种情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。

或者，你可以指定转换的数据，通过将 R 函数的自变量**rxDataStep**。 本教程中稍后提供这些操作的示例。

## <a name="next-step"></a>下一步

[查询和修改 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>上一步

[使用 SQL Server 数据使用 R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
