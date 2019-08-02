---
title: 在 Python 中使用输入和输出的快速入门
description: 在 SQL Server 中的 Python 脚本的此快速入门教程中, 了解如何构建 sp_execute_external_script 系统存储过程的输入和输出。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 10c62f78ff2ac23e33ad251a07ed8f3689f79843
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715467"
---
# <a name="quickstart-handle-inputs-and-outputs-using-python-in-sql-server"></a>快速入门：在 SQL Server 中使用 Python 处理输入和输出
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本快速入门演示了在 SQL Server 机器学习服务中使用 Python 时如何处理输入和输出。

默认情况下, [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)接受一个输入数据集, 该数据集通常以有效的 SQL 查询的形式提供。

其他类型的输入可以作为 SQL 变量传递: 例如, 可以使用序列化函数 (如[pickle](https://docs.python.org/3.0/library/pickle.html)或[rx_serialize_model](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-serialize-model) ) 以二进制格式编写模型, 作为变量传递定型模型。

该存储过程返回单个 Python [pandas](https://pandas.pydata.org/pandas-docs/stable/index.html)数据帧作为输出, 但您也可以将标量和模型输出为变量。 例如, 可以将定型模型输出为二进制变量并将其传递给 T-sql INSERT 语句, 以便将该模型写入表。 您还可以生成图形 (二进制格式) 或标量 (单个值, 例如日期和时间、训练模型所用的时间, 等等)。

## <a name="prerequisites"></a>先决条件

之前的快速入门,[请验证 SQL Server 中是否存在 python](quickstart-python-verify.md), 并提供设置此快速入门所需的 Python 环境所需的信息和链接。

## <a name="create-the-source-data"></a>创建源数据

通过运行以下 T-sql 语句来创建一个较小的测试数据表:

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

让我们看看 sp_execute_external_script 的默认输入和输出变量: `InputDataSet`和。 `OutputDataSet`

1. 可以从表中获取数据作为 Python 脚本的输入。 运行以下语句。 它从表中获取数据, 通过 Python 运行时进行往返, 并返回列名称为*NewColName*的值。

    查询返回的数据将传递到 Python 运行时, 这会将数据作为 pandas 数据帧返回到 SQL 数据库。 WITH RESULT SETS 子句定义了 SQL 数据库返回的数据表的架构。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'Python'
        , @script = N'OutputDataSet = InputDataSet;'
        , @input_data_1 = N'SELECT * FROM PythonTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **结果**

    ![从表返回数据的 Python 脚本的输出](./media/python-output-pythontestdata.png)

2. 让我们更改输入或输出变量的名称。 上面的脚本使用了默认输入和输出变量名称_InputDataSet_和_OutputDataSet_。 若要定义与_InputDataSet_关联的输入数据, 请使用 *@input_data_1* 变量。

    在此脚本中, 存储过程的输出和输入变量的名称已更改为*SQL_out*和*SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'Python'
      , @script = N'SQL_out = SQL_in'
      , @input_data_1 = N' SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    `@input_data_1_name`和`@script`中的输入和输出变量的大小写必须与 python 代码中的输入和输出变量大小写一致, 因为 python 区分大小写。 `@output_data_1_name`

    仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是, 你可以从 Python 代码内调用其他数据集, 还可以返回其他类型的输出和数据集。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。 

    `WITH RESULT SETS`语句定义 SQL Server 中使用的数据的架构。 需要为从 Python 返回的每个列提供 SQL 兼容的数据类型。 你可以使用架构定义来提供新的列名, 因为你不需要使用 Python 数据中的列名。

3. 你还可以使用 Python 脚本生成值, 并将输入查询字符串 _@input_data_1_ 留空。

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

    ![使用@script作为输入的查询结果](./media/python-data-generated-output.png)

## <a name="next-steps"></a>后续步骤

检查在 Python 和 SQL Server 之间传递表格数据时可能会遇到的一些问题。

> [!div class="nextstepaction"]
> [起步SQL Server 中的 Python 数据结构](quickstart-python-data-structures.md)
