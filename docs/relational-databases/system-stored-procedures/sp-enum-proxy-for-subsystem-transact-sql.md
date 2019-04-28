---
title: sp_enum_proxy_for_subsystem (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_enum_proxy_for_subsystem_TSQL
- sp_enum_proxy_for_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_proxy_for_subsystems
ms.assetid: 580cc3be-1068-4a96-8d15-78ca3a5bb719
ms.author: vanto
manager: craigg
ms.openlocfilehash: 5beab3dc255e5679191dd6ea5d05bfdd98bef6ba
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62723809"
---
# <a name="spenumproxyforsubsystem-transact-sql"></a>sp_enum_proxy_for_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理访问子系统所需的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_enum_proxy_for_subsystem  
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>参数  
`[ @proxy_id = ] proxy_id` 要列出信息的代理标识号。 *Proxy_id*是**int**，默认值为 NULL。 任一*id*或*proxy_name*可能指定。  
  
`[ @proxy_name = ] 'proxy_name'` 要列出信息的代理服务器的名称。 *Proxy_name*是**sysname**，默认值为 NULL。 任一*id*或*proxy_name*可能指定。  
  
`[ @subsystem_id = ] subsystem_id` 要列出信息的子系统的标识号。 *Subsystem_id*是**int**，默认值为 NULL。 任一*subsystem_id*或*subsystem_name*可能指定。  
  
`[ @subsystem_name = ] 'subsystem_name'` 要列出信息的子系统的名称。 *Subsystem_name*是**sysname**，默认值为 NULL。 任一*subsystem_id*或*subsystem_name*可能指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**subsystem_id**|**int**|子系统标识号。|  
|**subsystem_name**|**sysname**|子系统的名称。|  
|**proxy_id**|**int**|代理服务器标识号。|  
|**proxy_name**|**sysname**|代理服务器的名称。|  
  
## <a name="remarks"></a>备注  
 如果不提供任何参数， **sp_enum_proxy_for_subsystem**列出为每个子系统的实例中的所有代理有关的信息。  
  
 如果提供代理 id 或代理名称， **sp_enum_proxy_for_subsystem**列表子系统的代理服务器具有访问权限。 如果提供子系统 id 或子系统名称， **sp_enum_proxy_for_subsystem**列出有权访问该子系统的代理。  
  
 当同时提供代理信息和子系统信息时，如果指定的代理有权访问指定的子系统，则结果集将返回一行。  
  
 此存储的过程位于**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-all-associations"></a>A. 列出所有关联  
 以下示例列出了在当前实例的代理和子系统之间建立的所有权限。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem ;  
GO  
```  
  
### <a name="b-determining-if-a-proxy-has-access-to-a-specific-subsystem"></a>B. 确定代理是否有权访问特定的子系统  
 如果代理 `Catalog application proxy` 有权访问 `ActiveScripting` 子系统，则以下示例将返回一行。 否则，该示例将返回空结果集。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_proxy_for_subsystem  
    @subsystem_name = 'ActiveScripting',  
    @proxy_name = 'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_grant_proxy_to_subsystem &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
