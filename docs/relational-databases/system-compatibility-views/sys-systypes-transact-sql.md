---
title: sys.systypes (Transact SQL) |Microsoft Docs
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: edcf376f9127ec1d9b874c24e0a11f67f7e334ff
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43074144"
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
|**xusertype**|**smallint**|扩展用户类型。 如果数据类型的数字超过 32,767，则溢出或返回 NULL。|  
|**长度**|**smallint**|数据类型的物理长度。|  
|**xprec**|**tinyint**|服务器使用的内部精度。 不在查询中使用。|  
|**xscale**|**tinyint**|服务器使用的内部小数位数。 不在查询中使用。|  
|**tdefault**|**int**|特定存储过程的 ID，此存储过程包含对该数据类型的完整性检查功能。|  
|**域**|**int**|特定存储过程的 ID，此存储过程包含对该数据类型的完整性检查功能。|  
|**uid**|**smallint**|所有者类型的架构 ID。<br /><br /> 对于从旧版 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 升级的数据库，架构 ID 等于所有者的用户 ID。<br /><br /> **\*\* 重要\* \*** 如果您使用任何以下[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]DDL 语句，则必须使用[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目录视图，而不是**sys.systypes**。<br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> 如果用户数和角色数超过 32,767，则发生溢出或返回 NULL。|  
|**保留**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**collationid**|**int**|如果基于字符， **collationid**是当前数据库中; 的排序规则的 id，否则，则为 NULL。|  
|**usertype**|**smallint**|用户类型 ID。 如果数据类型的数字超过 32,767，则溢出或返回 NULL。|  
|variable|**bit**|可变长度数据类型。<br /><br /> 1 = True<br /><br /> 0 = False|  
|**allownulls**|**bit**|指示此数据类型的默认为空性。 如果为 null 性指定通过使用此默认值通过[CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md)或[ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。|  
|**类型**|**tinyint**|物理存储数据类型。|  
|**printfmt**|**varchar(255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**prec**|**smallint**|此数据类型的精度级别。<br /><br /> -1 = **xml**或大值类型。|  
|**scale**|**tinyint**|此数据类型根据精度确定的小数位数。<br /><br /> NULL = 数据类型不是数值。|  
|**排序规则**|**sysname**|如果基于字符，**排序规则**是排序规则的当前数据库中; 否则为，则为 NULL。|  
  
## <a name="see-also"></a>请参阅  
 [兼容性视图&#40;Transact SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [系统表映射到系统视图&#40;Transact SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
