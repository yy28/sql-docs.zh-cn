---
title: 使用 R 中的输入和输出的快速入门
description: 在 SQL Server 中的 R 脚本入门教程中, 了解如何构建 sp_execute_external_script 系统存储过程的输入和输出。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 1ccdf5206f2564ead2ca66f40143aee1b4ab1fad
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344622"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>快速入门：在 SQL Server 中使用 R 处理输入和输出
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本快速入门演示如何在 SQL Server 机器学习服务或 R Services 中使用 R 时处理输入和输出。

如果要在 SQL Server 中运行 R 代码, 则必须在存储过程中包装 R 脚本。 可以编写一个脚本, 也可以将 R 脚本传递给[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 此系统存储过程用于在 SQL Server 的上下文中启动 R 运行时, 将数据传递给 R, 并安全地管理 R 用户会话, 并将所有结果返回给客户端。

默认情况下, [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)接受一个输入数据集, 该数据集通常以有效的 SQL 查询的形式提供。 其他类型的输入可以作为 SQL 变量传递。

该存储过程返回单个 R 数据帧作为输出, 但您也可以将标量和模型输出为变量。 例如, 可以将定型模型输出为二进制变量并将其传递给 T-sql INSERT 语句, 以便将该模型写入表。 您还可以生成图形 (二进制格式) 或标量 (单个值, 例如日期和时间、训练模型所用的时间, 等等)。

## <a name="prerequisites"></a>先决条件

以前的快速入门,[验证 SQL Server 中是否存在 r](quickstart-r-verify.md), 提供了设置本快速入门所需的 R 环境的信息和链接。

## <a name="create-the-source-data"></a>创建源数据

通过运行以下 T-sql 语句来创建一个较小的测试数据表:

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

让我们看看 sp_execute_external_script 的默认输入和输出变量: `InputDataSet`和。 `OutputDataSet`

1. 可以从表中获取数据作为 R 脚本的输入。 运行以下语句。 它从表中获取数据, 通过 R 运行时进行一次往返, 并返回列名称为*NewColName*的值。

    查询返回的数据将传递给 R 运行时, 这会将数据作为数据帧返回到 SQL 数据库。 WITH RESULT SETS 子句定义了 SQL 数据库返回的数据表的架构。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N'OutputDataSet <- InputDataSet;'
        , @input_data_1 = N'SELECT * FROM RTestData;'
    WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    **结果**

    ![从表返回数据的 R 脚本的输出](./media/r-output-rtestdata.png)

2. 让我们更改输入或输出变量的名称。 上面的脚本使用了默认输入和输出变量名称_InputDataSet_和_OutputDataSet_。 若要定义与_InputDatSet_关联的输入数据, 请使用 *@input_data_1* 变量。

    在此脚本中, 存储过程的输出和输入变量的名称已更改为*SQL_out*和*SQL_in*:

    ```sql
    EXECUTE sp_execute_external_script
      @language = N'R'
      , @script = N' SQL_out <- SQL_in;'
      , @input_data_1 = N'SELECT 12 as Col;'
      , @input_data_1_name  = N'SQL_in'
      , @output_data_1_name =  N'SQL_out'
      WITH RESULT SETS (([NewColName] INT NOT NULL));
    ```

    请注意, R 区分大小写, 因此`@input_data_1_name`和`@output_data_1_name`中的输入和输出变量的大小写必须与中`@script`r 代码中的变量匹配。 

    仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是，可以从 R 代码内调用其他数据集，并且除数据集以外，还可以返回其他类型的输出。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。 

    `WITH RESULT SETS`语句定义 SQL Server 中使用的数据的架构。 需要为从 R 返回的每个列提供 SQL 兼容的数据类型。你可以使用架构定义来提供新的列名, 因为你不需要使用 R 数据帧中的列名称。

3. 你还可以使用 R 脚本生成值, 并将输入查询字符串 _@input_data_1_ 留空。

    ```sql
    EXECUTE sp_execute_external_script
        @language = N'R'
        , @script = N' mytextvariable <- c("hello", " ", "world");
            OutputDataSet <- as.data.frame(mytextvariable);'
        , @input_data_1 = N''
    WITH RESULT SETS (([Col1] CHAR(20) NOT NULL));
    ```

    **结果**

    ![使用@script作为输入的查询结果](./media/r-data-generated-output.png)

## <a name="next-steps"></a>后续步骤

检查在 R 和 SQL Server 之间传递数据时可能会遇到的一些问题, 例如, 在 R 和 SQL 之间的表格数据中的隐式转换和差异。

> [!div class="nextstepaction"]
> [起步处理数据类型和对象](quickstart-r-data-types-and-objects.md)