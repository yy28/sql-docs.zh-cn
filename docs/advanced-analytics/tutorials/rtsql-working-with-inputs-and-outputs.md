---
title: 快速入门： 使用输入和输出在 R 中 （SQL Server 机器学习） |Microsoft Docs
description: 在 SQL Server 中的 R 脚本的本快速入门，了解如何构建输入和输出到 sp_execute_external_script 系统存储过程。
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/15/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: b41a8c30cd0ecbe040819478c0cadece1b9eb704
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/17/2018
ms.locfileid: "39086579"
---
# <a name="quickstart-handle-inputs-and-outputs-using-r-in-sql-server"></a>快速入门： 处理输入和输出在 SQL Server 中使用 R
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

当你想要在 SQL Server 中运行 R 代码时，必须在存储过程中包装 R 脚本。 可以编写一个，也可以传递到 R 脚本[sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 此系统存储的过程用于在 SQL Server，将数据传递到 R，上下文中启动 R 运行时，安全地管理 R 用户会话，并向客户端返回任何结果。

## <a name="prerequisites"></a>必要條件

上一个快速入门中， [Hello World R 和 SQL 中](rtsql-using-r-code-in-transact-sql-quickstart.md)、 提供的信息和链接设置为本快速入门所需的 R 环境。

<a name="bkmk_SSMSBasics"></a>

## <a name="create-some-simple-test-data"></a>创建一些简单的测试数据

通过运行以下 T-SQL 语句来创建小型测试数据的表：

```sql
CREATE TABLE RTestData ([col1] int not null) ON [PRIMARY]
INSERT INTO RTestData   VALUES (1);
INSERT INTO RTestData   VALUES (10);
INSERT INTO RTestData   VALUES (100) ;
GO
```

成功创建表后，使用以下语句对表进行查询：
  
```sql
SELECT * FROM RTestData
```

**结果**

![RTestData 表的内容](media/quickstart-r-working-input-outputs-results-1.png)


## <a name="get-the-same-data-using-r-script"></a>使用 R 脚本获取相同的数据

成功创建表后，运行以下语句：

```sql
EXECUTE sp_execute_external_script
      @language = N'R'
    , @script = N' OutputDataSet <- InputDataSet;'
    , @input_data_1 = N' SELECT *  FROM RTestData;'
    WITH RESULT SETS (([NewColName] int NOT NULL));
```

它从表中获取数据，使 R 运行时，通过一次往返过程并返回具有列名称，值*NewColName*。

**结果**

![rsql_basictut_getsamedataR](media/rsql-basictut-getsamedatar.PNG)


**注释**

+ *@language* 参数定义本例中要调用 R 的语言扩展。
+ 在 *@script* 参数中，定义要传递给 R 运行时的命令。 必须以 Unicode 文本形式将整个 R 脚本封装在此参数中。 还可将文本添加到 **nvarchar** 类型的变量并调用该变量。
+ 查询返回的数据将传递给 R 运行时，后者将数据以数据框架的形式返回给 SQL Server。
+ WITH RESULT SETS 子句为 SQL Server 定义返回的数据表的架构。

## <a name="change-input-or-output-variables"></a>更改输入或输出变量

前面的示例使用了默认的输入和输出变量名称 _InputDataSet_ 与 _OutputDataSet_。 若要定义与 _InputDatSet_ 关联的输入数据，请使用 *@input_data_1* 变量。

在此示例中，存储过程的输出变量和输入变量名称已更改为 *SQL_Out* 和 *SQL_In*：

```sql
EXECUTE sp_execute_external_script
  @language = N'R'
  , @script = N' SQL_out <- SQL_in;'
  , @input_data_1 = N' SELECT 12 as Col;'
  , @input_data_1_name  = N'SQL_In'
  , @output_data_1_name =  N'SQL_Out'
  WITH RESULT SETS (([NewColName] int NOT NULL));
```

未收到错误，"对象 SQL\_中找不到"？ 这是因为 R 区分大小写！ 在本示例中，R 脚本使用变量 *SQL_in* 和 *SQL_out*，但存储过程的参数使用变量 *SQL_In* 和 *SQL_Out*。

请尝试纠正**仅** *SQL_In*变量*@script* ，然后重新运行存储的过程。

现在，您得到**不同**错误：

```Error
EXECUTE statement failed because its WITH RESULT SETS clause specified 1 result set(s), but the statement only sent 0 result set(s) at run time.
```

我们显示此错误因为你可能需要经常测试新的 R 代码时看到它。 这意味着，R 脚本已成功运行，但 SQL Server 接收到任何数据，或接收到错误或意外数据。

在本例中，输出架构（以 **WITH** 开头的行）指定应返回一个整数数据列，但由于 R 将数据放在不同的变量中，因此未向 SQL Server 返回任何结果，从而发生该错误。 若要修复此错误，更正第二个变量名称。

**请注意，这些要求 ！**

- 变量名称必须遵循有效 SQL 标识符的规则。
- 参数的顺序非常重要。 必须先指定必需的参数 *@input_data_1* 和 *@output_data_1*，然后才能使用可选参数 *@input_data_1_name* 和 *@output_data_1_name*。
- 仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是，可以从 R 代码内调用其他数据集，并且除数据集以外，还可以返回其他类型的输出。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。 本教程稍后提供了一个简单的示例。
- `WITH RESULT SETS` 语句定义数据的架构，为 SQL Server 提供优势。 对于从 R.返回的每个列，需要提供 SQL 兼容的数据类型。也可以使用架构定义来提供新的列名；不需要使用 R data.frame 中的列名。 在某些情况下，此子句是可选的;请尝试省略它，看看效果。

## <a name="generate-results-using-r"></a>使用 R 生成结果

还可以仅使用 R 脚本来生成值，并将 _@input_data_1_ 中的输入查询字符串留空。 或者，使用有效的 SQL SELECT 语句作为占位符，但不要在 R 脚本中使用 SQL 结果。

```sql
EXECUTE sp_execute_external_script
    @language = N'R'
   , @script = N' mytextvariable <- c("hello", " ", "world");
       OutputDataSet <- as.data.frame(mytextvariable);'
   , @input_data_1 = N' SELECT 1 as Temp1'
   WITH RESULT SETS (([Col1] char(20) NOT NULL));
```

**结果**

![使用查询结果@script作为输入](media/quickstart-r-working-input-outputs-results-3.png)

## <a name="next-steps"></a>后续步骤

检查某些 R 和 SQL Server 之间传递数据，例如隐式转换和表格数据的 R 和 SQL 之间的差异时可能遇到的问题。

> [!div class="nextstepaction"]
> [快速入门： 处理的数据类型和对象](../tutorials/rtsql-r-and-sql-data-types-and-data-objects.md)