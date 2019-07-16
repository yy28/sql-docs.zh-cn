---
title: sys.dm_clr_loaded_assemblies (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1cd677e516048aa52badec7fc9875e5a5b13f25a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138660"
---
# <a name="sysdmclrloadedassemblies-transact-sql"></a>sys.dm_clr_loaded_assemblies (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为加载到服务器地址空间的每个托管用户程序集返回一行。 使用此视图，以了解和解决问题 CLR 集成托管数据库对象中执行[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 程序集是用于定义托管数据库对象并在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中部署的托管代码 DLL 文件。 只要用户执行了这些托管数据库对象中的一个，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 CLR 便会加载其中定义了托管数据库对象的程序集（及其引用）。 将加载的程序集保留在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中可提高性能，以便将来可调用程序集中包含的托管数据库对象而无需重新加载该程序集。 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 面临内存不足的压力时才会卸载该程序集。 有关程序集和 CLR 集成的详细信息，请参阅[CLR 宿主环境](../../relational-databases/clr-integration/clr-integration-architecture-clr-hosted-environment.md)。 有关托管的数据库对象的详细信息，请参阅[使用公共语言运行时生成数据库对象&#40;CLR&#41;集成](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)。  

  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|已加载程序集的 ID。 **Assembly_id**可用于查找有关中的程序集的详细信息[sys.assemblies &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)目录视图。 请注意， [!INCLUDE[tsql](../../includes/tsql-md.md)] [sys.assemblies](../../relational-databases/system-catalog-views/sys-assemblies-transact-sql.md)目录显示在当前数据库中的程序集。 **Sqs.dm_clr_loaded_assemblies**视图显示服务器上所有已加载的程序集。|  
|**appdomain_address**|**int**|应用程序域的地址 (**AppDomain**) 在程序集加载。 单个用户拥有的所有程序集始终都在同一个加载**AppDomain**。 **Appdomain_address**可用于查找有关的详细信息**AppDomain**中[sys.dm_clr_appdomains](../../relational-databases/system-dynamic-management-views/sys-dm-clr-appdomains-transact-sql.md)视图。|  
|**load_time**|**datetime**|程序集的加载时间。 请注意，该程序集保留才能加载[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有内存压力和卸载**AppDomain**。 你可以监视**load_time**若要了解频率[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内存不足压力和卸载**AppDomain**。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="remarks"></a>备注  
 **Dm_clr_loaded_assemblies.appdomain_address**视图之间存在多对一关系与**dm_clr_appdomains.appdomain_address**。 **Dm_clr_loaded_assemblies.assembly_id**视图之间存在一个对多关系与**sys.assemblies.assembly_id**。  
  
## <a name="examples"></a>示例  
 以下示例显示如何查看当前加载的数据库中所有程序集的详细信息。  
  
```  
 SELECT a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
FROM sys.dm_clr_loaded_assemblies AS l   
INNER JOIN sys.assemblies AS a  
ON l.assembly_id = a.assembly_id;  
```  
  
 下面的示例演示如何查看的详细信息**AppDomain**在给定的程序集加载。  
  
```  
SELECT appdomain_id, creation_time, db_id, user_id, state  
FROM sys.dm_clr_appdomains AS a  
WHERE appdomain_address =   
(SELECT appdomain_address   
 FROM sys.dm_clr_loaded_assemblies  
 WHERE assembly_id = 555);  
```  
  
## <a name="see-also"></a>请参阅  
 [公共语言运行时与相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
