---
title: "CHECKSUM_AGG (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
caps.latest.revision: 38
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b202009c2920dfbcdd068ec3d7ab95de13caa7b4
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回组中各值的校验和。 Null 值会被忽略。 可以后接[OVER 子句](../../t-sql/queries/select-over-clause-transact-sql.md)。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>参数  
**ALL**  
向所有值应用此聚合函数。 ALL 为默认值。
  
DISTINCT  
指定 CHECKSUM_AGG 返回唯一校验值。
  
*expression*  
是一个整数[表达式](../../t-sql/language-elements/expressions-transact-sql.md)。 不允许使用聚合函数和子查询。
  
## <a name="return-types"></a>返回类型
返回所有的校验和*表达式*值作为**int**。
  
## <a name="remarks"></a>注释  
CHECKSUM_AGG 可用于检测表中的更改。
  
表中行的顺序不影响 CHECKSUM_AGG 的结果。 此外，CHECKSUM_AGG 函数还可与 DISTINCT 关键字和 GROUP BY 子句一起使用。
  
如果表达式列表中的某个值发生更改，则列表的校验和通常也会更改。 但只在极少数情况下，校验和会保持不变。
  
CHECKSUM_AGG 与其他聚合函数具有相似的功能。 有关详细信息，请参阅[聚合函数 &#40;Transact SQL &#41;](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>示例  
以下示例使用 `CHECKSUM_AGG` 检测 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中 `Quantity` 表的 `ProductInventory` 列中的更改。
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  
--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>另请参阅
[校验和 &#40;Transact SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[通过子句 &#40;Transact SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  

