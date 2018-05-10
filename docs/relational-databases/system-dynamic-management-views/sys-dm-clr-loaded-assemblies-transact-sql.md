---
title: sys.dm_clr_loaded_assemblies (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_clr_loaded_assemblies
- sys.dm_clr_loaded_assemblies_TSQL
- dm_clr_loaded_assemblies_TSQL
- sys.dm_clr_loaded_assemblies
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_loaded_assemblies dynamic management view
ms.assetid: 8523d8db-d8a0-4b1f-ae19-6705d633e0a6
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 66188678f31440327da37ae8591c9c64af33605c
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为加载到服务器地址空间的每个托管用户程序集返回一行。 使用此视图以了解和解决 CLR 集成管理在中执行的数据库对象[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 程序集是用于定义托管数据库对象并在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中部署的托管代码 DLL 文件。 只要用户执行了这些托管数据库对象中的一个，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 便会加载其中定义了托管数据库对象的程序集（及其引用）。 将加载的程序集保留在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可提高性能，以便将来可调用程序集中包含的托管数据库对象而无需重新加载该程序集。 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 面临内存不足的压力时才会卸载该程序集。 有关程序集和 CLR 集成的详细信息，请参阅[CLR 托管环境](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)。 有关托管的数据库对象的详细信息，请参阅[与公共语言运行时生成数据库对象&#40;CLR&#41;集成](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|已加载程序集的 ID。 **Assembly_id**可用于查找有关中的程序集的详细信息[sys.assemblies &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)目录视图。 请注意， [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)目录显示当前数据库中的程序集。 **Sqs.dm_clr_loaded_assemblies**视图会显示服务器上所有已加载的程序集。|  
|**appdomain_address**|**int**|应用程序域的地址 (**AppDomain**) 在程序集被加载。 单个用户所拥有的所有程序集始终都在同一个加载**AppDomain**。 **Appdomain_address**可以用于查找有关的详细信息**AppDomain**中[sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)视图。|  
|**load_time**|**datetime**|程序集的加载时间。 请注意，该程序集保持加载直到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有内存压力和卸载**AppDomain**。 你可以监视**load_time**频率了解[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内存紧张和卸载**AppDomain**。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="remarks"></a>注释  
 **Dm_clr_loaded_assemblies.appdomain_address**视图具有多对一关系**dm_clr_appdomains.appdomain_address**。 **Dm_clr_loaded_assemblies.assembly_id**视图具有一个对多关系**sys.assemblies.assembly_id**。  
  
## <a name="examples"></a>示例  
 以下示例显示如何查看当前加载的数据库中所有程序集的详细信息。  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 下面的示例演示如何以查看详细信息**AppDomain**中给定的程序集被加载。  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>另请参阅  
 [公共语言运行时相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
