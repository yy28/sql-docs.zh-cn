---
title: sys.database_scoped_configurations (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 01/16/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 015db41a34cdc4f22db79328e91189a77a483418
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdatabasescopedconfigurations-transact-sql"></a>sys.database_scoped_configurations (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  包含每个配置的一行。 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**configuration_id**|**int**|配置选项的 ID。|  
|**名称**|**nvarchar(60)**|配置选项的名称。 有关可能的配置信息，请参阅[ALTER DATABASE SCOPED CONFIGURATION &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)。|  
|**值**|**sqlvariant**|对于主副本的此配置选项设置的值。|  
|**value_for_secondary**|**sqlvariant**|为辅助副本此配置选项设置的值。|  
  
##  <a name="Permissions"></a> 权限  
 要求 **公共** 角色具有成员身份。  
  
## <a name="remarks"></a>注释  
 当为的值返回 NULL **value_for_secondary**，这意味着到辅助数据库已设置到主副本。  
 
 数据库作用域内配置设置随数据库一同转入。 这意味着还原或附加给定数据库时，会保留现有配置设置。
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)  
  
  
