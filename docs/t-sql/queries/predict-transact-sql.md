---
title: "预测 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- PREDICT
- PREDICT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- PREDICT clause
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 529cb229b6658085d0f2122604a4ed638f66a84c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="predict-transact-sql"></a>预测 (Transact SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

生成预测的值或基于存储模型的分数。  

## <a name="syntax"></a>语法

```
PREDICT  
(  
  MODEL = @model | model_literal,  
  DATA = object AS <table_alias>  
)  
WITH ( <result_set_definition> )  

<result_set_definition> ::=  
  {  
    { column_name  
      data_type  
      [ COLLATE collation_name ]  
      [ NULL | NOT NULL ]  
    }  
      [,...n ]  
  }  

MODEL = @model | model_literal  
```

### <a name="arguments"></a>参数

**model**

`MODEL`参数用于指定用于评分或预测的模型。 模型指定为变量或文字或标量表达式。

可以通过使用 R 或 Python 或其他工具创建的模型对象。

**数据**

数据参数用于指定用于评分或预测的数据。 在查询中的表源的形式指定数据。 表源可以是表、 表别名，CTE 别名、 视图或表值函数。

**参数**

参数参数用于指定用于评分或预测的可选用户定义参数。

每个参数的名称是特定于模型类型。 例如，在 RevoScaleR rxPredict 函数支持参数_@computeResiduals位_以支持剩余的计算，则在评分逻辑回归模型时。  你可以将传递到值参数名称和它`PREDICT`函数。

> [注意]此选项中的 SQL Server 自 2017 年的预发行版不支持而且包含仅用于向前兼容性。

**使用 ( \<result_set_definition >)**

WITH 子句用于指定由返回的输出的架构`PREDICT`函数。

除了返回的列`PREDICT`函数本身，所有的列的数据的一部分输入可用于在查询中使用。

### <a name="return-values"></a>返回值

没有预定义的架构是可用;SQL Server 不会验证模型的内容，并不验证返回的列的值。  
- `PREDICT`列通过传递作为输入的函数  
- `PREDICT`函数也会生成新列，但列数以及它们的数据类型取决于用于预测的模型的类型。  

与数据相关的任何错误消息，该模型或列格式返回与模型关联的基础预测函数。  
- 对于 RevoScaleR，等效的函数是[rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)  
- 对于 MicrosoftML，等效的函数是[rxPredict.mlModel](https://docs.microsoft.com/r-server/r-reference/microsoftml/rxpredict)  

不能查看内部模型结构使用`PREDICT`。 如果你想要了解模型本身的内容，必须加载的模型对象、 反序列化，并使用相应的 R 代码分析模型。

## <a name="remarks"></a>注释

`PREDICT`函数支持在所有版本的 SQL Server，包括 Linux。

不需要在要使用的服务器上安装 R、 Python 或另一台机器学习语言`PREDICT`函数。 可以在另一个环境中的对模型进行训练，还可以将其保存到与一起使用的 SQL Server 表`PREDICT`，或从另一个已保存的模型的 SQL Server 实例中调用模型。

### <a name="supported-algorithms"></a>支持的算法

你使用的模型必须已创建使用 RevoScaleR 包从支持的算法之一。 有关当前支持的型号的列表，请参阅[实时评分](../../advanced-analytics/real-time-scoring.md)。

### <a name="permissions"></a>Permissions

不所需的任何权限`PREDICT`; 但是，用户需求`EXECUTE`对数据库的权限和权限来查询任何用作输入的数据。 如果已在表中存储的模型，用户还必须能够从表中读取模型。

## <a name="examples"></a>示例

下面的示例演示调用的语法`PREDICT`。

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>调用存储的模型并将其用于预测

此示例调用存储在表 [models_table] 中的现有逻辑回归模型。 获取最新经过训练的模型，使用 SELECT 语句，并随后将二进制模型传递给预测函数。 输入的值表示功能;输出表示分配由模型的分类。

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 @model from [models_table]";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>在 FROM 子句中使用预测

此示例引用`PREDICT`函数中`FROM`子句`SELECT`语句：

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

别名**d**为表源指定_数据_参数用于引用属于 dbo.mytable 的列。 别名**p**指定的**预测**函数用于引用预测函数返回的列。

### <a name="combining-predict-with-an-insert-statement"></a>将与 INSERT 语句结合使用预测

预测的常见使用案例之一是生成输入数据的评分，然后将插入表中的预测的值。 下面的示例假定，调用应用程序使用存储的过程插入到表中包含的预测的值的行：

```sql
CREATE PROCEDURE InsertLoanApplication
(@p1 varchar(100), @p2 varchar(200), @p3 money, @p4 int)
AS
BEGIN
  DECLARE @model varbinary(max) = (select model
  FROM scoring_model
  WHERE model_name = 'ScoringModelV1');
  WITH d as ( SELECT * FROM (values(@p1, @p2, @p3, @p4)) as t(c1, c2, c3, c4) )

  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = d) WITH(score float) as p;
END;
```

如果该过程将通过表值参数的多个行，然后它可以进行编写，如下所示：

```sql
CREATE PROCEDURE InsertLoanApplications (@new_applications dbo.loan_application_type)
AS
BEGIN
  DECLARE @model varbinary(max) = (SELECT model_bin FROM scoring_models WHERE model_name = 'ScoringModelV1');
  INSERT INTO loan_applications (c1, c2, c3, c4, score)
  SELECT d.c1, d.c2, d.c3, d.c4, p.score
  FROM PREDICT(MODEL = @model, DATA = @new_applications as d)
  WITH (score float) as p;
END;
```

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>创建 R 模型和生成评分使用可选的模型参数

> [!NOTE]
> 在候选发布版 1 中不支持使用参数自变量。

此示例假定你已创建逻辑回归模型拟合的协方差矩阵，与使用对 RevoScaleR 这样的调用：

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

如果采用二进制格式，可以在 SQL Server 中存储模型，你可以使用预测函数来生成不只是预测，但支持的模型类型，如错误或置信度间隔的其他信息。

下面的代码演示从 R 到 rxPredict 等价的调用：

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

等效的调用使用`PREDICT`函数还提供了分数 （预测值），错误和置信度间隔：

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```



