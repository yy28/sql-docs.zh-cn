---
title: "SCHEMA_ID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SCHEMA_ID
- SCHEMA_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- identification numbers [SQL Server], schemas
- schemas [SQL Server], IDs
- SCHEMA_ID function
- IDs [SQL Server], schemas
- default schema IDs
ms.assetid: c8e34df5-3eea-459f-ae40-050909ce9fda
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: 6034b43145cf81c23359149b07f3b6caaffcc352
ms.contentlocale: zh-cn
ms.lasthandoff: 10/17/2017

---
# <a name="schemaid-transact-sql"></a>SCHEMA_ID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回与架构名称关联的架构 ID。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
SCHEMA_ID ( [ schema_name ] )   
```  
  
## <a name="arguments"></a>参数  
  
|术语|定义|  
|----------|----------------|  
|*schema_name*|是的架构的名称。 *schema_name*是**sysname**。 如果*schema_name*未指定，则 SCHEMA_ID 将返回调用方的默认架构的 ID。|  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 如果将返回 NULL *schema_name*不是有效的架构。  
  
## <a name="remarks"></a>注释  
 SCHEMA_ID 将返回系统架构的 ID 和用户定义架构的 ID。 SCHEMA_ID 可以在选择列表、WHERE 子句和任何允许使用表达式的地方调用。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-the-default-schema-id-of-a-caller"></a>A. 返回调用方的默认架构 ID  
  
```  
SELECT SCHEMA_ID();  
```  
  
### <a name="b-returning-the-schema-id-of-a-named-schema"></a>B. 返回命名架构的架构 ID  
  
```  
SELECT SCHEMA_ID('dbo');  
```  
  
## <a name="see-also"></a>另请参阅  
 [元数据函数 &#40;Transact SQL &#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME &#40;Transact SQL &#41;](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  


