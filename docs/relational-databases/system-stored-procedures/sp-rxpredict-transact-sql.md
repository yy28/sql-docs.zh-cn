---
title: sp_rxPredict |Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_rxPredict procedure
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 8f46403afef0e2f6cf967561a8fd24ec6409fe93
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434857"
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

生成基于机器学习模型存储在 SQL Server 数据库中的二进制格式中的给定输入的预测的值。

提供了 R 和 Python 机器学习模型中近实时地评分。 `sp_rxPredict` 为提供包装的存储的过程`rxPredict`中的 R 函数[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)并[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)，和[rx_predict](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-predict) Python 函数中[revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)并[microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)。 它在 C + 编写，并且专门针对计分操作进行了优化。

**本文适用于**:  
- SQL Server 2017  
- 使用 SQL Server 2016 R Services[升级 R 组件](https://docs.microsoft.com/sql/advanced-analytics/r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server)

## <a name="syntax"></a>语法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>参数

**model**

预先训练的模型中受支持的格式。 

**input**

有效的 SQL 查询

### <a name="return-values"></a>返回值

返回评分列，以及输入的数据源中的任何传递列。
其他评分列，如置信区间，则可以算法是否支持生成这样的值返回。

## <a name="remarks"></a>Remarks

若要启用的存储过程的使用，必须在实例上启用 SQLCLR。

> [!NOTE]
> 在启用此选项之前，请考虑的安全隐患。

用户需求`EXECUTE`针对数据库的权限。

### <a name="supported-platforms"></a>支持的平台
 
- SQL Server 2017 机器学习服务 （包括 R Server 9.2）  
- SQL Server 2017 机器学习服务器 （独立版） 
- SQL Server R Services 2016，进行到 R Server 9.1.0 的 R Services 实例的升级或更高版本  

### <a name="supported-algorithms"></a>支持的算法

有关受支持的算法的列表，请参阅[实时评分](../../advanced-analytics/real-time-scoring.md)。

以下模型类型都**不**支持：  
- 模型包含其他、 不受支持类型的 R 转换  
- 使用情况建模`rxGlm`或`rxNaiveBayes`RevoScaleR 中的算法  
- PMML 模型  
- 使用其他 R 库从 CRAN 或其他存储库中创建的模型  
- 包含此处未列出的其他 R 任何的转换其他类型的模型  

## <a name="examples"></a>示例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了成为有效的 SQL 查询中的输入数据*@inputData*必须包括在存储模型中的列与列兼容。

`sp_rxPredict` 仅支持以下.NET 列类型： 双精度型、 float、 short、 ushort、 long、 ulong 和字符串。 您可能需要筛选出输入数据中不支持的类型，然后再使用它进行实时评分。 

  有关相应 SQL 类型的信息，请参阅[SQL-CLR 类型映射](/dotnet/framework/data/adonet/sql/linq/sql-clr-type-mapping)或[映射 CLR 参数数据](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

