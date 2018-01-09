---
title: "sp_rxPredict |Microsoft 文档"
ms.custom: 
ms.date: 07/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_rxPredict
- sp_rxPredict_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_rxPredict procedure
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d2bf07247f63962e5692325e2e7518a78445f0a8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="sprxpredict"></a>sp_rxPredict  
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

生成基于存储模型的预测的值。

提供在机器学习模型中几乎实时上评分。 `sp_rxPredict`为存储的过程用作包装器`rxPredict`函数中[RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)和[MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)。 它用 C + 编写的并专门针对计分操作进行了优化。 它支持这两个 R 或 Python 机器学习模型。

**本主题适用于**:  
- SQL Server 2017  
- SQL Server 2016 升级到 Microsoft R Server R Services  

## <a name="syntax"></a>语法

```
sp_rxPredict  ( @model, @input )
```

### <a name="arguments"></a>参数

**model**

中受支持的格式的预先训练的模型。 

**输入**

有效的 SQL 查询

### <a name="return-values"></a>返回值

返回评分列，以及输入的数据源的任何传递列。
其他评分列，如置信度间隔，可以如果该算法支持生成此类值返回。

## <a name="remarks"></a>Remarks

若要启用的存储过程的使用，必须在实例上启用 SQLCLR。

> [!NOTE]
> 在启用此选项之前，请考虑的安全隐患。

用户需求`EXECUTE`对数据库拥有权限。

### <a name="supported-platforms"></a>支持的平台

需要以下版本之一：  
- SQL Server 自 2017 年 1 机器学习服务 （包括 Microsoft R Server 9.1.0）  
- Microsoft 机器学习服务器  
- SQL Server R Services 2016，与 Microsoft R Server 9.1.0 到的 R Services 实例的升级或更高版本  

### <a name="supported-algorithms"></a>支持的算法

有关支持的算法的列表，请参阅[实时评分](../../advanced-analytics/real-time-scoring.md)。

以下模型类型**不**支持：  
- 模型包含其他、 不受支持类型的 R 转换  
- 模型使用`rxGlm`或`rxNaiveBayes`中 RevoScaleR 算法  
- PMML 模型  
- 使用其他 R 库从 CRAN 或其他存储库创建的模型  
- 模型包含任何其他类型的 R 之外此处列出的转换  

## <a name="examples"></a>示例

```sql
DECLARE @model = SELECT @model 
FROM model_table 
WHERE model_name = 'rxLogit trained';

EXEC sp_rxPredict @model = @model,
@inputData = N'SELECT * FROM data';
```

除了成为有效的 SQL 查询中的输入数据 *@inputData* 必须在存储模型中包括列与列兼容。

`sp_rxPredict`仅支持以下.NET 列类型： 双精度型、 float、 short、 ushort，long、 ulong 和字符串。 你可能需要使用实时评分之前筛选出你输入的数据中不支持的类型。 

  有关相应 SQL 类型的信息，请参阅[SQL CLR 类型映射](https://msdn.microsoft.com/library/bb386947.aspx)或[映射 CLR 参数数据](../clr-integration-database-objects-types-net-framework/mapping-clr-parameter-data.md)。

