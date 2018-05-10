---
title: PREDICT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2018
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: b027530565b9b138d5a8f9559e3e60e0331dd3af
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="predict-transact-sql"></a>PREDICT (Transact-SQL)  
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

基于存储模型生成预测值或评分。  

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

`MODEL` 参数用于指定用于评分或预测的模型。 将模型指定为变量或文字或标量表达式。

可以通过使用 R 或 Python 或其他工具创建模型对象。

data

DATA 参数用于指定用于评分或预测的数据。 在查询中以表源的形式指定数据。 表源可以是表、表别名、CTE 别名、视图或表值函数.

**参数**

PARAMETERS 参数用于指定用于评分或预测的可选用户定义参数。

每个参数的名称特定于模型类型。 例如，RevoScaleR 中的 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 函数支持参数 `@computeResiduals`，指示在对逻辑回归模型评分时是否应计算残差。 如果正在调用兼容模型，无法将该参数名称和 TRUE 或 FALSE 值传递到 `PREDICT` 函数。

> [!NOTE]
> 此选项在 SQL Server 2017 的预发行版本中无效。

WITH ( <result_set_definition> )

WITH 子句用于指定 `PREDICT` 函数返回的输出的架构。

除了 `PREDICT` 函数本身返回的列之外，所有在数据输入中包含的列都可以在查询中使用。

### <a name="return-values"></a>返回值

没有可用的预定义架构，SQL Server 不验证模型的内容，且不验证返回的列值。

- `PREDICT` 函数作为输入通过列传递。
- `PREDICT` 函数还生成新列，但列数以及其数据类型取决于用于预测的模型类型。

任何与数据、模型或列格式相关的错误消息都由与模型关联的基础预测函数返回。

- 对于 RevoScaleR，等效的函数是 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)  
- 对于 MicrosoftML，等效的函数是 [rxPredict.mlModel](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/rxpredict)  

不能使用 `PREDICT` 查看内部模型结构。 如果要了解模型本身的内容，必须加载模型对象，将其反序列化，然后使用相应的 R 代码来分析模型。

## <a name="remarks"></a>Remarks

无论是否启用其他机器学习功能，所有版本的 SQL Server（包括 Linux 和 Azure SQL 数据库）都支持 `PREDICT` 函数。 但需要 SQL Server 2017 或更高版本。 

不需要在服务器上安装 R、Python 或另一种机器学习语言就可以使用 `PREDICT` 函数。 可以在另一个环境中对模型进行训练，还可以将其保存到 SQL Server 表中以与 `PREDICT` 结合使用，或从另一个已保存该模型的 SQL Server 实例中调用该模型。

### <a name="supported-algorithms"></a>支持的算法

使用的模型必须是使用 RevoScaleR 包中支持的算法之一创建的。 有关当前支持的型号的列表，请参阅[实时评分](../../advanced-analytics/real-time-scoring.md)。

### <a name="permissions"></a>权限

`PREDICT` 不需要任何权限；但是，用户需要数据库 `EXECUTE` 权限，以及查询用作输入的任何数据的权限。 如果模型已存储在表中，则用户还须能够从表中读取模型。

## <a name="examples"></a>示例

以下示例展示了调用 `PREDICT` 的语法。

### <a name="call-a-stored-model-and-use-it-for-prediction"></a>调用存储的模型并将其用于预测

此示例调用存储在表 [models_table] 中的现有逻辑回归模型。 它使用 SELECT 语句获取最新经过训练的模型，并随后将二进制模型传递给 PREDICT 函数。 输入值表示功能；输出值表示由模型分配的分类。

```sql
DECLARE @logit_model varbinary(max) = "SELECT TOP 1 [model_binary] from [models_table] ORDER BY [trained_date] DESC";
DECLARE @input_qry = "SELECT ID, [Gender], [Income] from NewCustomers";

SELECT PREDICT [class]
FROM PREDICT( MODEL = @logit_model,  DATA = @input_qry
WITH (class string);
```

### <a name="using-predict-in-a-from-clause"></a>在 FROM 子句中使用 PREDICT

此示例引用 `SELECT` 语句的 `FROM` 子句中的 `PREDICT` 函数：

```sql
SELECT d.*, p.Score
FROM PREDICT(MODEL = @logit_model, 
  DATA = dbo.mytable AS d) WITH (Score float) AS p;
```

`DATA` 参数中为表源指定的别名 d 用于引用属于 dbo.mytable 的列。 为 PREDICT 函数指定的别名 p 用于引用 PREDICT 函数返回的列。

### <a name="combining-predict-with-an-insert-statement"></a>将 PREDICT 与 INSERT 语句相结合

常见的预测使用案例之一是生成输入数据的评分，然后将预测值插入到表中。 下面的示例假定，应用程序调用操作会使用存储过程将包含预测值的行插入到表中：

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

如果该过程通过一个表值参数接受多个行，那么它可以编写如下：

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

### <a name="creating-an-r-model-and-generating-scores-using-optional-model-parameters"></a>创建 R 模型并使用可选模型参数生成评分

> [!NOTE]
> 候选发布版 1 不支持使用参数自变量。

此示例假定已使用对 RevoScaleR 的调用创建了一个拟合协方差矩阵的逻辑回归模型，如下所示：

```R
logitObj <- rxLogit(Kyphosis ~ Age + Start + Number, data = kyphosis, covCoef = TRUE)
```

如果采用二进制格式在 SQL Server 中存储模型，不仅可以使用 PREDICT 函数生成预测，还可以生成模型类型支持的其他信息，如错误或置信区间。

下面的代码演示 R 对 [rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict) 的等效调用：

```R
rxPredict(logitObj, data = new_kyphosis_data, computeStdErr = TRUE, interval = "confidence")
```

使用 `PREDICT` 函数的等效调用还提供评分（预测值）、错误和置信区间：

```sql
SELECT d.Age, d.Start, d.Number, p.pred AS Kyphosis_Pred, p.stdErr, p.pred_lower, p.pred_higher
FROM PREDICT( MODEL = @logitObj,  DATA = new_kyphosis_data AS d,
  PARAMETERS = N'computeStdErr bit, interval varchar(30)',
  computeStdErr = 1, interval = 'confidence')
WITH (pred float, stdErr float, pred_lower float, pred_higher float) AS p;
```
