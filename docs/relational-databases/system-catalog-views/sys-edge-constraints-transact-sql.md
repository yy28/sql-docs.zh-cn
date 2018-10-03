---
title: sys.edge_constraints (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 09/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.edge_constraints
- edge_constraints
- SQL Graph
- edge_constraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.edge_constraints catalog view
ms.assetid: 0f782d2f-7126-46ab-85b7-bcba44862231
author: shkale-msft
ms.author: shkale
manager: craigg
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4068b127bdf4563e18cb459781f8a9a98ced6230
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785115"
---
# <a name="sysedgeconstraints-transact-sql"></a>sys.edge_constraints (Transact SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

包含行的每个对象都是边缘约束。 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<从 sys.objects 继承的列 >**||此视图所继承的列的列表，请参阅[sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_disabled**|**bit**|1 = 禁用约束的边缘。<br /><br /> 0 = 启用约束的边缘。|  
|**is_not_trusted**|**bit**|1 = 的 edge 系统尚未验证约束。<br /><br /> 0 = 的 edge 系统验证约束。|  
|**delete_referential_action**|**tinyint**|已在此边缘约束定义的引用操作。<br /><br />0 = 没有操作。|  
|**delete_referential_action_desc**|**nvarchar(60)**|已在此边缘约束定义的引用操作的说明。<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = 约束名称由系统生成的边缘。<br /><br />0 = 的 edge 由用户提供约束的名称。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
