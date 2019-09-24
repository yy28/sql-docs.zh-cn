---
title: 创建并运行简单的 Python 脚本
titleSuffix: SQL Server Machine Learning Services
description: 使用 SQL Server 机器学习服务在 SQL Server 实例中创建和运行简单的 Python 脚本。
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6f7fe62f746a8f6e74ebdf9f766b76c0edc720a
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2019
ms.locfileid: "71204294"
---
# <a name="quickstart-create-and-run-simple-python-scripts-with-sql-server-machine-learning-services"></a>快速入门：利用 SQL Server 机器学习服务创建和运行简单的 Python 脚本
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中，你将使用[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)创建并运行一组简单的 Python 脚本。 你将了解如何在存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)中包装格式正确的 Python 脚本，并在 SQL Server 实例中执行该脚本。

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装了 Python 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)访问 SQL Server 的实例。

- 还需要一个用于运行包含 Python 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="run-a-simple-script"></a>运行简单脚本

若要运行 Python 脚本，需将其作为参数传递给系统存储过程[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。
此系统存储过程在 SQL Server 的上下文中启动 Python 运行时，将数据传递给 Python，安全地管理 Python 用户会话，并将所有结果返回到客户端。

在下面的步骤中，你将在你的 SQL Server 实例中运行下面的示例 Python 脚本：

```python
a = 1
b = 2
c = a/b
d = a*b
print(c, d)
```

1. 在连接到 SQL Server 实例**SQL Server Management Studio**中打开新的查询窗口。

1. 将完整的 Python 脚本传递给`sp_execute_external_script`存储过程。

   通过`@script`参数传递脚本。 参数内的`@script`所有内容都必须是有效的 Python 代码。

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. 计算正确的结果，Python `print`函数将结果返回到 "**消息**" 窗口。

   其外观应与下面类似。

    **结果**

    ```text
    STDOUT message(s) from external script:
    0.5 2
    ```

## <a name="run-a-hello-world-script"></a>运行 Hello World 脚本

典型的示例脚本是只输出字符串 "Hello World" 的脚本。 运行以下命令。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'OutputDataSet = InputDataSet'
    , @input_data_1 = N'SELECT 1 AS hello'
WITH RESULT SETS(([Hello World] INT));
GO
```

存储过程的`sp_execute_external_script`输入包括：

| | |
|-|-|
| @language | 定义要调用的语言扩展，在本例中为 Python |
| @script | 定义传递到 Python 运行时的命令<br>整个 Python 脚本必须以 Unicode 文本的形式包含在此参数中。 还可将文本添加到**nvarchar**类型的变量中，然后调用变量 |
| @input_data_1 | 查询返回的数据，传递到 Python 运行时，它将数据作为数据帧返回 SQL Server |
|WITH RESULT SETS | 子句定义为 SQL Server 返回的数据表的架构，在此示例中，将 "Hello World" 添加为列名称，并将**int**用于数据类型。 |

命令输出以下文本：

| 世界您好 |
|-------------|
| 1 |

## <a name="use-inputs-and-outputs"></a>使用输入和输出

默认情况下`sp_execute_external_script` ，接受单个数据集作为输入，该数据集通常以有效的 SQL 查询的形式提供。 然后，它返回单个 Python 数据帧作为输出。

现在，让我们使用的默认输入和输出变量`sp_execute_external_script`：**InputDataSet**和**OutputDataSet**。

1. 创建一个较小的测试数据表。

    ```sql
    CREATE TABLE PythonTestData (col1 INT NOT NULL)
    
    INSERT INTO PythonTestData
    VALUES (1);
    
    INSERT INTO PythonTestData
    VALUES (10);
    
    INSERT INTO PythonTestData
    VALUES (100);
    GO
    ```

1. `SELECT`使用语句查询表。
  
    ```sql
    SELECT *
    FROM PythonTestData
    ```

    **结果**

    ![PythonTestData 表的内容](./media/select-pythontestdata.png)

1. 运行以下 Python 脚本。 它使用`SELECT`语句从表中检索数据，通过 Python 运行时传递数据，并以数据帧的形式返回数据。 子句定义了 SQL 返回的数据表的架构，并添加了列名*NewColName。* `WITH RESULT SETS`

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    **结果**

    ![从表返回数据的 Python 脚本的输出](./media/python-output-pythontestdata.png)

1. 现在，更改输入和输出变量的名称。 默认的输入和输出变量名称为**InputDataSet**和**OutputDataSet**，以下脚本将名称更改为**SQL_in**和**SQL_out**：

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'SQL_out = SQL_in;'
        , @input_data_1 = N'SELECT 12 as Col;'
        , @input_data_1_name  = N'SQL_in'
        , @output_data_1_name = N'SQL_out'
    WITH RESULT SETS(([NewColName] INT NOT NULL));
    ```

    请注意，Python 区分大小写。 Python 脚本（**SQL_out**， **SQL_in**）中使用的输入和输出变量需要与和`@input_data_1_name` `@output_data_1_name`（包括大小写）一起定义的名称匹配。

   > [!TIP]
   > 仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是, 你可以从 Python 代码内调用其他数据集, 还可以返回其他类型的输出和数据集。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。

1. 你还可以使用没有输入数据的 Python 脚本生成值（`@input_data_1`设置为空白）。

   下面的脚本输出文本 "hello" 和 "world"。

   ```sql
   EXECUTE sp_execute_external_script @language = N'Python'
       , @script = N'
   import pandas as pd
   mytextvariable = pandas.Series(["hello", " ", "world"]);
   OutputDataSet = pd.DataFrame(mytextvariable);
   '
       , @input_data_1 = N''
   WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
   ```

   **结果**

   ![使用@script作为输入的查询结果](./media/python-data-generated-output.png)

> [!NOTE]
> Python 使用前导空格对语句进行分组。 因此，当嵌入的 Python 脚本跨越多行时（如前面的脚本中所述），请勿尝试将 Python 命令缩进到与 SQL 命令串联在一起。 例如，以下脚本将生成错误：

  ```text
  EXECUTE sp_execute_external_script @language = N'Python'
      , @script = N'
      import pandas as pd
      mytextvariable = pandas.Series(["hello", " ", "world"]);
      OutputDataSet = pd.DataFrame(mytextvariable);
      '
      , @input_data_1 = N''
  WITH RESULT SETS(([Col1] CHAR(20) NOT NULL));
  ```

## <a name="check-python-version"></a>检查 Python 版本

若要查看 SQL Server 实例中安装的 Python 版本，请运行以下脚本。

```sql
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import sys
print(sys.version)
'
GO
```

Python `print`函数将该版本返回到 "**消息**" 窗口。 在下面的示例输出中，可以看到，在这种情况下，将安装 Python 版本3.5.2。

**结果**

```text
STDOUT message(s) from external script: 
3.5.2 |Continuum Analytics, Inc.| (default, Jul  5 2016, 11:41:13) [MSC v.1900 64 bit (AMD64)]
```

## <a name="list-python-packages"></a>列出 Python 包

Microsoft 在 SQL Server 实例中提供了大量预安装了 SQL Server 机器学习服务的 Python 包。

若要查看安装了哪些 Python 包（包括版本）的列表，请运行以下脚本。

```SQL
EXECUTE sp_execute_external_script @language = N'Python'
    , @script = N'
import pip
for i in pip.get_installed_distributions():
    print(i)
'
GO
```

输出来自`pip.get_installed_distributions()` Python 中，并作为`STDOUT`消息返回。

**结果**

```text
STDOUT message(s) from external script:
xlwt 1.2.0
XlsxWriter 0.9.6
xlrd 1.0.0
win-unicode-console 0.5
widgetsnbextension 2.0.0
wheel 0.29.0
Werkzeug 0.12.1
wcwidth 0.1.7
unicodecsv 0.14.1
traitlets 4.3.2
tornado 4.4.2
toolz 0.8.2
. . .
```

## <a name="next-steps"></a>后续步骤

若要在 SQL Server 中使用 Python 创建机器学习模型，请按照以下快速入门：

> [!div class="nextstepaction"]
> [使用 SQL Server 机器学习服务在 Python 中创建和评分预测模型](quickstart-python-train-score-model.md)

有关 SQL Server 机器学习服务的详细信息，请参阅以下文章。

- [在 SQL Server 中使用 Python 处理数据类型和对象机器学习服务](quickstart-python-data-structures.md)
- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
