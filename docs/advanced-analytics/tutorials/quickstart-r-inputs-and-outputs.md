---
title: 快速入门： 使用输入和 R 的 SQL Server 机器学习中的输出
description: 在 SQL Server 中的 R 脚本的本快速入门，了解如何构建输入和输出到 sp_execute_external_script 系统存储过程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 56d2eb65ca95dd4f153f3c7a6ebb00e926465687
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046752"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>快速入门：处理输入和输出在 SQL Server 中使用 R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本快速入门演示如何处理输入和输出时使用 SQL Server 机器学习服务中的 R 或 R Services。

当你想要在 SQL Server 中运行 R 代码时，必须在存储过程中包装 R 脚本。 可以编写一个，也可以传递到 R 脚本[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 此系统存储的过程用于在 SQL Server，将数据传递到 R，上下文中启动 R 运行时，安全地管理 R 用户会话，并向客户端返回任何结果。

默认情况下[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)接受单个输入数据集，这通常中有效的 SQL 查询的形式提供。 作为 SQL 变量，可以传递其他类型的输入。

存储的过程返回单个 R 数据框架作为输出，但您也可以输出标量和作为变量的模型。 例如，可以输出为二进制变量已训练的模型，并将其传递给 T-SQL INSERT 语句，该模型写入表。 您还可以生成绘图 （以二进制格式） 或标量 （单个值，如日期和时间，经过的时间来训练该模型，等等）。

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 R](quickstart-r-verify.md)、 提供的信息和链接设置为本快速入门所需的 R 环境。

## <a name="create-the-source-data"></a>创建源数据

通过运行以下 T-SQL 语句来创建小型测试数据的表：

```sql
CREATE TABLE RTestData (col1 INT NOT NULL)
INSERT INTO RTestData VALUES (1);
INSERT INTO RTestData VALUES (10);
INSERT INTO RTestData VALUES (100);
GO
```

成功创建表后，使用以下语句对表进行查询：
  
```sql
SELECT * FROM RTestData
```

**结果**

![RTestData 表的内容](./media/select-rtestdata.png)

## <a name="inputs-and-outputs"></a>“脚本转换编辑器”

让我们看一下默认的 sp_execute_external_script 的输入和输出变量：`InputDataSet`和`OutputDataSet`。

1. 作为 R 脚本的输入，可以从表获取数据。 运行下面的语句。 它从表中获取数据，使 R 运行时，通过一次往返过程并返回具有列名称的值*NewColName*。

    由查询返回的数据传递给 R 运行时，将数据返回到 SQL 数据库作为数据帧。 WITH RESULT SETS 子句定义为 SQL 数据库返回的数据的表的架构。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **结果**

    ![返回表中的数据的 R 脚本输出](./media/r-output-rtestdata.png)

2. 让我们来更改输入或输出变量的名称。 上述脚本使用了默认的输入和输出变量名称， _InputDataSet_并_OutputDataSet_。 若要定义与关联的输入的数据_InputDatSet_，则使用*@input_data_1*变量。

    在此脚本中，存储过程的输出和输入的变量名称已更改为*SQL_out*并*SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    请注意，R 是区分大小写，因此输入和输出变量中的事例`@input_data_1_name`并`@output_data_1_name`必须匹配与中的 R 代码中的`@script`。 

    此外，参数的顺序非常重要。 必须先指定必需的参数 *@input_data_1* 和 *@output_data_1*，然后才能使用可选参数 *@input_data_1_name* 和 *@output_data_1_name*。

    仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是，可以从 R 代码内调用其他数据集，并且除数据集以外，还可以返回其他类型的输出。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。 

    `WITH RESULT SETS`语句在 SQL Server 中定义的数据使用的架构。 您需要为你从 R.返回每个列提供 SQL 兼容的数据类型可以使用的架构定义来提供新的列名称也不需要使用 R 数据帧中的列名称。

3. 此外可以生成使用 R 脚本的值，并保留中的输入的查询字符串_@input_data_1_保留为空。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **结果**

    ![使用查询结果@script作为输入](./media/r-data-generated-output.png)

## <a name="next-steps"></a>后续步骤

检查某些 R 和 SQL Server 之间传递数据，例如隐式转换和表格数据的 R 和 SQL 之间的差异时可能遇到的问题。

> [!div class="nextstepaction"]
> [快速入门：处理数据类型和对象](quickstart-r-data-types-and-objects.md)