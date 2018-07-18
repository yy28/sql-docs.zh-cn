---
title: sys.dm_clr_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f95f4d1596d84648034b51833738a26817f5e96b
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997999"
---
# <a name="sysdmclrproperties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  对于与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 公共语言运行时 (CLR) 集成相关的每个属性（包括宿主 CLR 的版本和状态）返回一行。 通过运行初始化宿主的 CLR [CREATE ASSEMBLY](../../t-sql/statements/create-assembly-transact-sql.md)， [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)，或[DROP ASSEMBLY](../../t-sql/statements/drop-assembly-transact-sql.md)语句，或通过执行任何 CLR 例程、 类型或触发器。 **Sys.dm_clr_properties**视图不指定是否已在服务器上启用用户 CLR 代码的执行。 通过启用用户 CLR 代码的执行[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)存储过程，并[clr 已启用](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)选项设置为 1。  
  
 **Sys.dm_clr_properties**视图包含**名称**并**值**列。 此视图中的每一行都提供了有关宿主 CLR 的某个属性的详细信息。 使用此视图搜集有关宿主 CLR 的信息，例如 CLR 安装目录、CLR 版本和宿主 CLR 的当前状态。 此视图可以帮助您确定 CLR 集成代码之所以无效是否是因为服务器上的 CLR 安装存在问题。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**名称**|**nvarchar(128)**|属性的名称。|  
|**value**|**nvarchar(128)**|属性的值。|  
  
## <a name="properties"></a>属性  
 **Directory**属性指示在服务器安装.NET Framework 的目录。 在服务器上可能存在多个 .NET Framework 安装，该属性的值标识了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 正在使用的安装。  
  
 **版本**属性指示.NET Framework 的版本和服务器上托管 CLR。  
  
 **Sys.dm_clr_properties**动态管理的视图可返回六个不同的值**状态**属性，用于反映状态[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]宿主 CLR。 它们分别是：  
  
-   Mscoree 未加载。  
  
-   Mscoree 已加载。  
  
-   带 mscoree 的锁定 CLR 版本。  
  
-   CLR 已初始化。  
  
-   CLR 初始化永久失败。  
  
-   CLR 已停止。  
  
 **Mscoree 未加载**并**Mscoree 已加载**状态在服务器启动时显示宿主 CLR 初始化的进度和不太可能出现。  
  
 **带 mscoree 的锁定 CLR 版本**其中未使用宿主的 CLR，因此，它具有尚未初始化，可能会看到状态。 初始化宿主的 CLR 第一次的 DDL 语句 (如[创建程序集&#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) 或执行托管的数据库对象。  
  
 **CLR 初始化**状态指示宿主的 CLR 已成功初始化。 请注意，这并不能指示是否启用了用户 CLR 代码的执行。 如果用户 CLR 代码的执行是第一个启用和使用，则禁用[!INCLUDE[tsql](../../includes/tsql-md.md)] [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)存储的过程，仍将是状态值**CLR 初始化**。  
  
 **CLR 初始化永久失败**状态指示宿主 CLR 初始化失败。 原因可能是内存不足，也可能是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 与 CLR 的宿主握手失败。 在此情况下，将引发错误消息 6512 或 6513。  
  
 **CLR 已停止状态**仅当出现[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]正在关闭。  
  
## <a name="remarks"></a>Remarks  
 属性和值的此视图中的未来版本可能会更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]由于 CLR 集成功能的增强功能。  
  
## <a name="permissions"></a>权限  
  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="examples"></a>示例  
 以下示例检索有关宿主 CLR 的信息：  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [公共语言运行时与相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
