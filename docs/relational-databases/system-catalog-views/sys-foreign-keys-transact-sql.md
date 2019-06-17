---
title: sys.foreign_keys (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- foreign_keys
- sys.foreign_keys
- sys.foreign_keys_TSQL
- foreign_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.foreign_keys catalog view
ms.assetid: e960df1a-13fc-43ee-ba91-34c1b719ac2c
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d1cceaf4c200f6fe9f2bf6c735548bc0f439dab7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465567"
---
# <a name="sysforeignkeys-transact-sql"></a>sys.foreign_keys (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  每个对象，它与 FOREIGN KEY 约束，存在对应的一行**sys.object.type** = f。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<从 sys.objects 继承的列 >**||此视图所继承的列的列表，请参阅[sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**referenced_object_id**|**int**|所引用对象的 ID。|  
|**key_index_id**|**int**|所引用对象内键索引的 ID。|  
|**is_disabled**|**bit**|禁用 FOREIGN KEY 约束。|  
|**is_not_for_replication**|**bit**|FOREIGN KEY 约束通过 NOT FOR REPLICATION 选项创建。|  
|**is_not_trusted**|**bit**|系统尚未验证 FOREIGN KEY 约束。|  
|**delete_referential_action**|**tinyint**|执行删除时为此 FOREIGN KEY 声明的引用操作。<br /><br /> 0 = 不执行任何操作<br /><br /> 1 = 级联<br /><br /> 2 = 设置 Null<br /><br /> 3 = 设置默认值|  
|**delete_referential_action_desc**|**nvarchar(60)**|执行删除时为此 FOREIGN KEY 声明的引用操作的说明：<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**update_referential_action**|**tinyint**|执行更新时为此 FOREIGN KEY 声明的引用操作。<br /><br /> 0 = 不执行任何操作<br /><br /> 1 = 级联<br /><br /> 2 = 设置 Null<br /><br /> 3 = 设置默认值|  
|**update_referential_action_desc**|**nvarchar(60)**|执行更新时为此 FOREIGN KEY 声明的引用操作的说明：<br /><br /> NO_ACTION<br /><br /> CASCADE<br /><br /> SET_NULL<br /><br /> SET_DEFAULT|  
|**is_system_named**|**bit**|1 = 名称由系统生成。<br /><br /> 0 = 名称由用户提供。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
