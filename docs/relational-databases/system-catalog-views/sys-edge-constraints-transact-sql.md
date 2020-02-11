---
title: sys. edge_constraints （Transact-sql） |Microsoft Docs
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
monikerRange: '>=sql-server-2017||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5dc2e47c49dc9d639489426fceab0b848c9def3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68079318"
---
# <a name="sysedge_constraints-transact-sql"></a>sys. edge_constraints （Transact-sql）
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx.md](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

对于作为边缘约束的每个对象都包含一行。 
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**\<继承自 sys.databases 的列>**||有关此视图所继承的列的列表，请参阅[sys.databases &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)。|  
|**is_disabled**|**bit**|1 = Edge 约束为禁用。<br /><br /> 0 = 启用边缘约束。|  
|**is_not_trusted**|**bit**|1 = 系统未验证边缘约束。<br /><br /> 0 = 边缘约束已由系统验证。|  
|**delete_referential_action**|**tinyint**|在此边缘约束上定义的引用操作。<br /><br />0 = 不执行任何操作。|  
|**delete_referential_action_desc**|**nvarchar （60）**|在此边缘约束上定义的引用操作的说明。<br /><br />NO_ACTION|  
|**is_system_named**|**bit**|1 = 边缘约束名是由系统生成的。<br /><br />0 = 边缘约束名称由用户提供。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的对象目录视图](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
