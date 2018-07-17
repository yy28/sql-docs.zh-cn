---
title: SCHEMA_ID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 12d21a3532d196461d65b3d405918627606c7c43
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2018
ms.locfileid: "37792218"
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
|*schema_name*|是架构的名称。 schema_name 为 sysname。 如果未指定 schema_name，则 SCHEMA_ID 将返回调用方的默认架构的 ID。|  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
 如果 schema_name 不是有效架构，将返回 NULL。  
  
## <a name="remarks"></a>Remarks  
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
 [元数据函数 (Transact-SQL)](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SCHEMA_NAME (Transact-SQL)](../../t-sql/functions/schema-name-transact-sql.md)   
 [sys.schemas (Transact-SQL)](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)  
  
  

