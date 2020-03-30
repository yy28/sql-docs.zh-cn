---
title: 快速入门：运行 R 脚本
description: 使用 SQL Server 机器学习服务运行一组简单的 R 脚本。 了解如何在 SQL Server 实例中使用存储过程 sp_execute_external_script 执行该脚本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/27/2020
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 495bb56cf76391c8baa1734665d5064b586d4be8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2020
ms.locfileid: "76831783"
---
# <a name="quickstart-run-simple-r-scripts-with-sql-server-machine-learning-services"></a>快速入门：通过 SQL Server 机器学习服务运行简单的 R 脚本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中，将使用 [SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)运行一组简单的 R 脚本。 你将了解如何在 SQL Server 实例中使用存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 执行该脚本。

## <a name="prerequisites"></a>先决条件

- 本快速入门需要使用安装了 R 语言的 [SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 实例。

  SQL Server 实例可以位于 Azure 虚拟机中，也可以位于本地。 请注意，默认情况下禁用外部脚本编写功能，因此可能需要在开始之前[启用外部脚本编写](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证 SQL Server Launchpad 服务是否正在运行  。

- 你还需要一个工具来运行包含 R 脚本的 SQL 查询。 可使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，并运行 T-SQL 查询或存储过程即可。 本快速入门使用 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="run-a-simple-script"></a>运行简单脚本

若要运行 R 脚本，请将它作为参数传递给系统存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
此系统存储过程在 SQL Server 的上下文中启动 R 运行时，将数据传递给 R，安全地管理 R 用户会话并将任何结果返回给客户端。

在下面的步骤中，在 SQL Server 实例中运行此示例 R 脚本：

```r
a <- 1
b <- 2
c <- a/b
d <- a*b
print(c(c, d))
```

1. 打开 SQL Server Management Studio 并连接到 SQL Server 实例  。

1. 将完整的 R 脚本传递到 `sp_execute_external_script` 存储过程。

   通过 `@script` 参数传递脚本。 `@script` 参数内的所有内容都必须是有效的 R 代码。

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

1. 计算出正确的结果，R `print` 函数将结果返回到“消息”窗口  。

   结果应该如下所示。

    **结果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>运行 Hello World 脚本

典型的示例脚本只输出字符串“Hello World”。 运行以下命令。

```sql
EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'OutputDataSet<-InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

`sp_execute_external_script` 存储过程的输入包括：

| | |
|-|-|
| @language | 定义本例中要调用 R 的语言扩展 |
| @script | 定义传递给 R 运行时的命令。 必须将整个 R 脚本作为 Unicode 文本包括在此参数中。 还可将文本添加到 nvarchar 类型的变量并调用该变量  |
| @input_data_1 | 查询返回的数据将传递给 R 运行时，后者将数据以数据框架的形式返回给 SQL Server |
|WITH RESULT SETS | 子句为 SQL Server 定义返回的数据表的架构，并将“Hello World”添加为列名称且 int 为数据类型  |

命令输出以下文本：

| Hello World |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>使用输入和输出

默认情况下，`sp_execute_external_script` 接受单个数据集作为输入，通常以有效的 SQL 查询的形式提供。 然后，它返回单个 R 数据帧作为输出。

现在，使用 `sp_execute_external_script` 的默认输入和输出变量：InputDataSet 和 OutputDataSet   。

1. 创建一个小型测试数据表。

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

1. 使用 `SELECT` 语句来查询表。
  
    ```sql
    SELECT *
    FROM RTestData
    ```

    **结果**

    ![RTestData 表的内容](./media/select-rtestdata.png)

1. 运行以下 R 脚本。 它使用 `SELECT` 语句从表中检索数据，通过 R 运行时传递数据，并以数据帧的形式返回数据。 `WITH RESULT SETS` 子句为 SQL 定义返回的数据表的架构，并添加了列名称“NewColName”  。

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **结果**

    ![从表返回数据的 R 脚本的输出](./media/r-output-rtestdata.png)

1. 现在，更改输入变量和输出变量的名称。 默认的输入和输出变量名称是 InputDataSet 和 OutputDataSet，而此脚本会将名称更改为 SQL_in 和 SQL_out     ：

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N' SQL_out <- SQL_in;'
        , @input_data_1 = N' SELECT 12 as Col;'
        , @input_data_1_name = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    请注意 R 区分大小写。 R 脚本中使用的输入和输出变量（SQL_out、SQL_in）需要匹配使用 `@input_data_1_name` 和 `@output_data_1_name` 定义的名称，包括大小写   。

   > [!TIP]
   > 只能将一个输入数据集作为参数传递，并且只能返回一个数据集。 但是，可以从 R 代码内部调用其他数据集，并且可以返回除数据集之外的其他类型的输出。 也可向任何参数添加 OUTPUT 关键字，让该参数随结果一起返回。

1. 还可以仅使用没有输入数据的 R 脚本（`@input_data_1` 设置为空白）生成值。

   以下脚本输出文本“hello”和“world”。

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

R `print` 函数将该版本返回到“消息”窗口  。 在下面的示例输出中，可以看到本例中安装的是 R 版本 3.4.4。

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

Microsoft 提供了许多随 SQL Server 机器学习服务预安装的 R 包。

若要查看已安装的 R 包列表（包括版本、依赖项、许可证和库路径的信息），请运行以下脚本。

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

输出来自 R 中的 `installed.packages()`，并作为结果集返回。

**结果**

![R 中安装的包](./media/rsql-installed-packages.png) 

## <a name="next-steps"></a>后续步骤

若要了解在 SQL Server 机器学习服务中使用 R 时如何使用数据结构，请遵循此快速入门：

> [!div class="nextstepaction"]
> [在 SQL Server 机器学习服务中使用 R 处理数据类型和对象](quickstart-r-data-types-and-objects.md)

有关在 SQL Server 机器学习服务中使用 R 的详细信息，请参阅以下文章：

- [使用 SQL Server 机器学习服务编写高级 R 函数](quickstart-r-functions.md)
- [通过 SQL Server 机器学习服务在 R 中创建预测模型并对其进行评分](quickstart-r-train-score-model.md)
- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
