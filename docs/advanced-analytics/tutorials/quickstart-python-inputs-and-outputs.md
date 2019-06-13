---
title: 使用输入和输出 Python-SQL Server 机器学习中的快速入门
description: 在 SQL Server 中的 Python 脚本本快速入门，了解如何构建输入和输出到 sp_execute_external_script 系统存储过程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fe60197671e40317f56a62ad98ea364a238df174
ms.sourcegitcommit: c3de32efeee3095fcea0d3faebb8f2ff1b56d229
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/12/2019
ms.locfileid: "67033387"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>快速入门：处理输入和输出在 SQL Server 中使用 Python
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本快速入门演示如何处理输入和输出时在 SQL Server 机器学习服务中使用 Python。

默认情况下[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)接受单个输入数据集，这通常中有效的 SQL 查询的形式提供。

可以作为 SQL 变量传递其他类型的输入： 例如，您可以传递训练的模型作为变量，如使用序列化函数[pickle](https://docs.python.org/3.0/library/pickle.html)或[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model)中编写模型二进制格式。

存储的过程返回单个 Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html)数据帧为 output，但您也可以输出标量和作为变量的模型。 例如，可以输出为二进制变量已训练的模型，并将其传递给 T-SQL INSERT 语句，该模型写入表。 您还可以生成绘图 （以二进制格式） 或标量 （单个值，如日期和时间，经过的时间来训练该模型，等等）。

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 Python](quickstart-python-verify.md)、 提供的信息和链接设置为本快速入门所需的 Python 环境。

## <a name="create-the-source-data"></a>创建源数据

通过运行以下 T-SQL 语句来创建小型测试数据的表：

```sql
CREATE TABLE PythonTestData (col1 INT NOT NULL)
INSERT INTO PythonTestData VALUES (1);
INSERT INTO PythonTestData VALUES (10);
INSERT INTO PythonTestData VALUES (100);
GO
```

成功创建表后，使用以下语句对表进行查询：
  
```sql
SELECT * FROM PythonTestData
```

**结果**

![PythonTestData 表的内容](./media/select-pythontestdata.png)

## <a name="inputs-and-outputs"></a>“脚本转换编辑器”

让我们看一下默认的 sp_execute_external_script 的输入和输出变量：`InputDataSet`和`OutputDataSet`。

1. 作为 Python 脚本的输入，可以从表获取数据。 运行下面的语句。 它从表中获取数据、 使通过 Python 运行时，一次往返过程并返回具有列名称的值*NewColName*。

    由查询返回的数据传递到 Python 运行时，将数据返回到 SQL 数据库作为 pandas 数据帧。 WITH RESULT SETS 子句定义为 SQL 数据库返回的数据的表的架构。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **结果**

    ![返回表中的数据的 Python 脚本输出](./media/python-output-pythontestdata.png)

2. 让我们来更改输入或输出变量的名称。 上述脚本使用了默认的输入和输出变量名称， _InputDataSet_并_OutputDataSet_。 若要定义与关联的输入的数据_InputDataSet_，则使用 *@input_data_1* 变量。

    在此脚本中，存储过程的输出和输入的变量名称已更改为*SQL_out*并*SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    中的输入和输出变量的大小写`@input_data_1_name`并`@output_data_1_name`一定要匹配的 Python 代码中的这种情况`@script`，如 Python 是区分大小写。

    仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是，您可以在 Python 代码内部调用从其他数据集，并且可以返回除数据集的其他类型的输出。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。 

    `WITH RESULT SETS`语句在 SQL Server 中定义的数据使用的架构。 需要提供 SQL 兼容的数据类型为从 Python 返回每个列。 可以使用的架构定义来提供新的列名称也不需要使用 Python data.frame 中的列名称。

3. 此外可以生成使用 Python 脚本的值，并保留中的输入的查询字符串 _@input_data_1_ 保留为空。

    ```sql
    EXECUTE sp_execute_external_script
    @language = N'Python'
    , @script = N'
    import pandas as pd
    mytextvariable = pandas.Series(["hello", " ", "world"]);
    OutputDataSet = pd.DataFrame(mytextvariable);'
    , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **结果**

    ![使用查询结果@script作为输入](./media/python-data-generated-output.png)

## <a name="next-steps"></a>后续步骤

检查某些 Python 和 SQL Server 之间传递的表格数据时可能遇到的问题。

> [!div class="nextstepaction"]
> [快速入门：SQL Server 中的 Python 数据结构](quickstart-python-data-structures.md)
