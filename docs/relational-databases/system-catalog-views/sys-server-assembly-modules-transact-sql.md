---
title: sys. server_assembly_modules （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: a814539e3b04135a5d97ad4d4d7b31546c88e62d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832726"
---
# <a name="sysserver_assembly_modules-transact-sql"></a>sys.server_assembly_modules (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  类型为 TA 的服务器级别触发器的每个程序集模块在表中对应一行。 此视图将程序集触发器映射到基础 CLR 实现。 可以将此关系联接到**sys.databases server_triggers**。 该程序集必须加载到**master**数据库中。 元组 (object_id) 是该关系的键。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|这是对定义此程序集模块所依据对象的反向 FOREIGN KEY 引用。|  
|**assembly_id**|**int**|创建此模块所基于的程序集的 ID。 此程序集必须加载到 master 数据库中。|  
|**assembly_class**|**sysname**|定义此模块的程序集内的类的名称。|  
|**assembly_method**|**sysname**|定义此模块的类中的方法的名称。 对于聚合函数 (AF)，该列为 NULL。|  
|**execute_as_principal_id**|**int**|EXECUTE AS 服务器主体的 ID。<br /><br /> 默认情况下，或者 EXECUTE AS CALLER 时，为 NULL。<br /><br /> 指定主体的 ID （如果 EXECUTE AS SELF EXECUTE AS \< principal>。<br /><br /> -2 = EXECUTE AS OWNER。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的目录视图 &#40;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
