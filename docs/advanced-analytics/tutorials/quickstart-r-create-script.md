---
title: 创建和运行简单的 R 脚本
titleSuffix: SQL Server Machine Learning Services
description: 使用 SQL Server 机器学习服务在 SQL Server 实例中创建和运行简单的 R 脚本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e49b01d3c3a4ac743d6614d66cc7864aee946460
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72006040"
---
# <a name="quickstart-create-and-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>快速入门：利用 SQL Server 机器学习服务创建和运行简单的 R 脚本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中，你将使用[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)创建并运行一组简单的 R 脚本。 你将了解如何在存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中包装格式正确的 R 脚本，并在 SQL Server 实例中执行该脚本。

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装 R 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)SQL Server 的实例。

  SQL Server 实例可位于 Azure 虚拟机或本地。 请注意，默认情况下禁用外部脚本功能，因此在开始之前，您可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证**SQL Server Launchpad 服务**是否正在运行。

- 还需要一个用于运行包含 R 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="run-a-simple-script"></a>运行简单脚本

若要运行 R 脚本，请将它作为参数传递给系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
此系统存储过程在 SQL Server 的上下文中启动 R 运行时，将数据传递给 R，安全地管理 R 用户会话，并将所有结果返回到客户端。

在下面的步骤中，你将在你的 SQL Server 实例中运行此示例 R 脚本：

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. 打开**SQL Server Management Studio** ，然后连接到 SQL Server 实例。

1. 将完整的 R 脚本传递到 @no__t 0 存储过程。

   通过 @no__t 参数传递脚本。 @No__t 参数内的所有内容都必须是有效的 R 代码。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. 计算正确的结果，并且 R `print` 函数将结果返回到 "**消息**" 窗口。

   其外观应与下面类似。

    **结果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>运行 Hello World 脚本

典型的示例脚本是只输出字符串 "Hello World" 的脚本。 运行以下命令。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

@No__t 0 存储过程的输入包括：

| | |
|-|-|
| @language | 定义要调用的语言扩展，在本例中为 R |
| @script | 定义传递给 R 运行时的命令。 必须以 Unicode 文本形式将整个 R 脚本封装在此参数中。 还可将文本添加到**nvarchar**类型的变量中，然后调用变量 |
| @input_data_1 | 查询返回的数据，传递给 R 运行时，它将数据作为数据帧返回 SQL Server |
|WITH RESULT SETS | 子句定义为 SQL Server 返回的数据表的架构，并将 "Hello World" 添加为列名称，为数据类型输入**int** |

命令输出以下文本：

| 世界您好 |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>使用输入和输出

默认情况下，`sp_execute_external_script` 接受单个数据集作为输入，通常以有效的 SQL 查询的形式提供。 然后，它返回单个 R 数据帧作为输出。

现在，让我们使用默认的输入和输出变量 `sp_execute_external_script`：**InputDataSet**和**OutputDataSet**。

1. 创建一个较小的测试数据表。

    ```sql
    CREATE TABLE RTestData (col1 INT NOT NULL)
    
    INSERT INTO RTestData
    VALUES (1);
    
    INSERT INTO RTestData
    VALUES (10);
    
    INSERT INTO RTestData
    VALUES (100);
    GO
    ```

1. 使用 `SELECT` 语句查询表。
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **结果**

    ![RTestData 表的内容](./media/select-rtestdata.png)

1. 运行以下 R 脚本。 它使用 `SELECT` 语句从表中检索数据，并通过 R 运行时传递数据，并以数据帧的形式返回数据。 @No__t-0 子句定义为 SQL 返回的数据表的架构，并添加列名称*NewColName*。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **结果**

    ![从表返回数据的 R 脚本的输出](./media/r-output-rtestdata.png)

1. 现在，让我们更改输入变量和输出变量的名称。 默认的输入和输出变量名称为**InputDataSet**和**OutputDataSet**，此脚本会将名称更改为**SQL_in**和**SQL_out**：

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    请注意，R 区分大小写。 R 脚本（**SQL_out**， **SQL_in**）中使用的输入和输出变量需要与使用 @no__t 2 和 @no__t （包括大小写）定义的名称匹配。

   > [!TIP]
   > 仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是，可以从 R 代码内调用其他数据集，并且除数据集以外，还可以返回其他类型的输出。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。

1. 你还可以使用没有输入数据的 R 脚本生成值（@no__t 设置为空白）。

   下面的脚本输出文本 "hello" 和 "world"。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    mytextvariable <- c("hello", " ", "world");
    OutputDataSet <- as.data.frame(mytextvariable);
    '
        , @input_data_1 = N''
    WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
    ```

    **结果**

    ![使用 @script 作为输入的查询结果](./media/r-data-generated-output.png)

## <a name="check-r-version"></a>检查 R 版本

若要查看 SQL Server 实例中安装的 R 版本，请运行以下脚本。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(version)';
GO
```

R `print` 函数将版本返回到 "**消息**" 窗口。 在下面的示例输出中，可以看到，在这种情况下，将安装 R 版本3.4.4。

**结果**

```text
STDOUT message(s) from external script:
                   _
platform       x86_64-w64-mingw32
arch           x86_64
os             mingw32
system         x86_64, mingw32
status
major          3
minor          4.4
year           2018
month          03
day            15
svn rev        74408
language       R
version.string R version 3.4.4 (2018-03-15)
nickname       Someone to Lean On
```

## <a name="list-r-packages"></a>列出 R 包

Microsoft 提供了许多与 SQL Server 机器学习服务预安装的 R 包。

若要查看已安装 R 包的列表，包括版本、依赖项、许可证和库路径信息，请运行以下脚本。

```SQL
EXEC sp_execute_external_script @language = N'R'
    , @script = N'
OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
WITH result sets((
            Package NVARCHAR(255)
            , Version NVARCHAR(100)
            , Depends NVARCHAR(4000)
            , License NVARCHAR(1000)
            , LibPath NVARCHAR(2000)
            ));
```

输出来自 R `installed.packages()`，作为结果集返回。

**结果**

![R 中安装的包](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>后续步骤

若要了解如何在 SQL Server 机器学习服务中使用 R 时使用数据结构，请按照以下快速入门：

> [!div class="nextstepaction"]
> [在 SQL Server 中使用 R 处理数据类型和对象机器学习服务](quickstart-r-data-types-and-objects.md)

有关在 SQL Server 机器学习服务中使用 R 的详细信息，请参阅以下文章：

- [通过 SQL Server 机器学习服务写入高级 R 函数](quickstart-r-functions.md)
- [使用 SQL Server 机器学习服务创建和评分预测模型](quickstart-r-train-score-model.md)
- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
