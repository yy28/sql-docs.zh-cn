---
title: sys.server_assembly_modules (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- server_assembly_modules_TSQL
- sys.server_assembly_modules
- server_assembly_modules
- sys.server_assembly_modules_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_assembly_modules catalog view
ms.assetid: af799e38-2d16-49b2-bcf5-6f9199af899e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a257f63328fe0abcf121b82b619bc58b70b7c6f7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47711697"
---
# <a name="sysserverassemblymodules-transact-sql"></a>sys.server_assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  类型为 TA 的服务器级别触发器的每个程序集模块在表中对应一行。 此视图将程序集触发器映射到基础 CLR 实现。 您可以加入到此关系**sys.server_triggers**。 程序集必须加载到**主**数据库。 元组 (object_id) 是该关系的键。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|这是对定义此程序集模块所依据对象的反向 FOREIGN KEY 引用。|  
|**assembly_id**|**int**|创建此模块所基于的程序集的 ID。 此程序集必须加载到 master 数据库中。|  
|**assembly_class**|**sysname**|定义此模块的程序集内的类的名称。|  
|**assembly_method**|**sysname**|定义此模块的类中的方法的名称。 对于聚合函数 (AF)，该列为 NULL。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 服务器主体的 ID。<br /><br /> 默认情况下，或者 EXECUTE AS CALLER 时，为 NULL。<br /><br /> 指定主体 if 的 ID 执行 AS SELF EXECUTE AS\<主体 >。<br /><br /> -2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
