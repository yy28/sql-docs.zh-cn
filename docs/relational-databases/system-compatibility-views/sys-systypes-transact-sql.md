---
title: sys.systypes (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.systypes_TSQL
- systypes_TSQL
- sys.systypes
- systypes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.systypes compatibility view
- systypes system table
ms.assetid: 1b0b1d0c-5f7b-470b-bd52-8bfa922d7889
caps.latest.revision: 50
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8526b0335d9d222cd0c28f4304566812905a07b7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="syssystypes-transact-sql"></a>sys.systypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为数据库中定义的每种系统提供的数据类型和每种用户定义的数据类型返回一行。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**sysname**|数据类型名称。|  
|**xtype**|**tinyint**|物理存储类型。|  
|**status**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**int**|扩展用户类型。 如果数据类型的数字超过 32,767，则溢出或返回 NULL。|  
|**length**|**int**|数据类型的物理长度。|  
|**xprec**|**tinyint**|服务器使用的内部精度。 不在查询中使用。|  
|**xscale**|**tinyint**|服务器使用的内部小数位数。 不在查询中使用。|  
|**tdefault**|**int**|特定存储过程的 ID，此存储过程包含对该数据类型的完整性检查功能。|  
|**域**|**int**|特定存储过程的 ID，此存储过程包含对该数据类型的完整性检查功能。|  
|**uid**|**int**|所有者类型的架构 ID。<br /><br /> 对于从旧版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级的数据库，架构 ID 等于所有者的用户 ID。<br /><br /> **\*\* 重要\* \*** 如果你使用以下任一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DDL 语句，您必须使用[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目录视图，而不是**sys.systypes**。<br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> 如果用户数和角色数超过 32,767，则发生溢出或返回 NULL。|  
|**保留**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**collationid**|**int**|如果基于字符， **collationid**是当前数据库中; 的排序规则的 id 否则，它为 NULL。|  
|**usertype**|**int**|用户类型 ID。 如果数据类型的数字超过 32,767，则溢出或返回 NULL。|  
|variable|**bit**|可变长度数据类型。<br /><br /> 1 = True<br /><br /> 0 = False|  
|**allownulls**|**bit**|指示此数据类型的默认为空性。 如果通过使用指定为 null，则通过覆盖此默认值[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)或[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。|  
|**类型**|**tinyint**|物理存储数据类型。|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**int**|此数据类型的精度级别。<br /><br /> 为-1 = **xml**或较大的值类型。|  
|**小数位数**|**tinyint**|此数据类型根据精度确定的小数位数。<br /><br /> NULL = 数据类型不是数值。|  
|**排序规则**|**sysname**|如果基于字符，**排序规则**是的排序规则的当前数据库中; 否则，它为 NULL。|  
  
## <a name="see-also"></a>另请参阅  
 [兼容性视图&#40;Transact SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [将系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
