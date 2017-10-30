---
title: "SCHEMA_NAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_NAME
- SCHEMA_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SCHEMA_NAME function
- schemas [SQL Server], names
ms.assetid: 20071b77-2b6e-4ce7-a8e3-fa71480baf73
caps.latest.revision: 27
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: bbc8d08ff59f85544fe3f11712c6780431bc76d7
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="schemaname-transact-sql"></a>SCHEMA_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回与架构 ID 关联的架构名称。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SCHEMA_NAME ( [ schema_id ] )  
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|----------|----------------|  
|*schema_id*|架构的 ID。 *schema_id*是**int**。如果*schema_id*是未定义，SCHEMA_NAME 将返回调用方的默认架构的名称。|  
  
## <a name="return-types"></a>返回类型  
 **sysname**  
  
 时，则返回 NULL *schema_id*不是有效的 id。  
  
## <a name="remarks"></a>注释  
 SCHEMA_NAME 返回系统架构和用户定义架构的名称。 可以在选择列表、WHERE 子句和任何允许使用表达式的地方调用 SCHEMA_NAME。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-name-of-the-default-schema-of-the-caller"></a>A. 返回调用方的默认架构的名称  
  
```  
SELECT SCHEMA_NAME();  
```  
  
### <a name="b-returning-the-name-of-a-schema-by-using-an-id"></a>B. 使用 ID 返回架构的名称  
  
```  
SELECT SCHEMA_NAME(1);  
```  
  
## <a name="see-also"></a>另请参阅  
 [表达式 &#40;Transact SQL &#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [SCHEMA_ID &#40;Transact SQL &#41;](../../t-sql/functions/schema-id-transact-sql.md)   
 [sys.schemas &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [其中 &#40;Transact SQL &#41;](../../t-sql/queries/where-transact-sql.md)  
  
  


