---
title: "使用输入和输出（T-SQL 中的 R 教程）|Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 75480e5c-f37f-45b9-a176-67e08e9a9daf
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 1e98d521cc4e8b637d686ec9cf7f47b03f4c728d
ms.lasthandoff: 04/11/2017

---
# <a name="working-with-inputs-and-outputs-r-in-t-sql-tutorial"></a>使用输入和输出（T-SQL 中的 R 教程）
如果想要在 SQL Server 中运行 R 代码，必须将 R 脚本包装在系统存储过程 [sp_execute_external_script](https://msdn.microsoft.com/library/mt604368.aspx) 中。 此存储过程用于在 SQL Server 的上下文中启动 R 运行时，然后，R 运行时将数据传递给 R、安全管理 R 用户会话，并向客户端返回任何结果。 


## <a name="bkmk_SSMSBasics"></a>创建一些简单的测试数据 
  
运行以下 T-SQL 语句来创建一个小型的测试数据表。     
   
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
  
|col1|
|------|
|*1*|   
|*10*|   
|*100*|   
  
    
## <a name="get-the-same-data-using-r-script"></a>使用 R 脚本获取相同的数据    
  
创建表后，运行以下语句。 该语句从表中获取数据、通过 R 运行时执行往返访问，然后返回包含列名 *NewColName* 的值。   
  
```sql    
EXECUTE sp_execute_external_script    
      @language = N'R'    
    , @script = N' OutputDataSet <- InputDataSet;'    
    , @input_data_1 = N' SELECT *  FROM RTestData;'    
    WITH RESULT SETS (([NewColName] int NOT NULL));
```    
**结果**

![rsql_basictut_getsamedataR](../../advanced-analytics/r-services/media/rsql-basictut-getsamedatar.PNG)

**说明**    


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

出现了此错误？ 

  *eval(expr, envir, enclos) 出错: 找不到对象 'SQL_in'*

这是因为 R 区分大小写！ 在本示例中，R 脚本使用变量 *SQL_in* 和 *SQL_out*，但存储过程的参数使用变量 *SQL_In* 和 *SQL_Out*。 

请只尝试纠正 *SQL_In* 变量，然后重新运行存储过程。 现在，会出现一个不同的错误：

  *EXECUTE 语句失败，因为其 WITH RESULT SETS 子句指定了 1 个结果集，但该语句在运行时仅发送了 0 个结果集。*

这是测试 R 代码时经常会看到的一般性错误。 这意味着，R 脚本已成功运行，但 SQL Server 未返回任何数据，或者返回了错误或意外的数据。 在本例中，输出架构（以 **WITH** 开头的行）指定应返回一个整数数据列，但由于 R 将数据放在不同的变量中，因此未向 SQL Server 返回任何结果，从而发生该错误。  

- 变量名称必须遵循有效 SQL 标识符的规则。 
- 参数的顺序非常重要。 必须先指定必需的参数 *@input_data_1* 和 *@output_data_1*，然后才能使用可选参数 *@input_data_1_name* 和 *@output_data_1_name*。     
- 仅可将一个输入数据集作为参数传递，且仅可返回一个数据集。 但是，可以从 R 代码内调用其他数据集，并且除数据集以外，还可以返回其他类型的输出。 还可以向任何参数添加 OUTPUT 关键字，使其随结果一起返回。 本教程稍后提供了一个简单的示例。      
- `WITH RESULT SETS` 语句定义数据的架构，为 SQL Server 提供优势。 对于从 R.返回的每个列，需要提供 SQL 兼容的数据类型。也可以使用架构定义来提供新的列名；不需要使用 R data.frame 中的列名。 在某些情况下，此子句是可选的；请尝试省略它，看看会发生什么情况。    
- 在 Management Studio 中，表格结果在“值”窗格中返回。 R 运行时返回的消息在“消息”窗格中提供。     
  
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
   
*Col1*     
*hello*    
<code>   </code>         
*world*    
    

## <a name="next-step"></a>下一步

接下来将探讨在 R 与 SQL Server 之间传递数据时可能会遇到的一些问题，例如，R 与 SQL 之间表格数据的隐式转换和差异。 

[R 和 SQL 的数据类型与数据对象](../../advanced-analytics/r-services/r-and-sql-data-types-and-data-objects-r-in-t-sql-tutorial.md)


