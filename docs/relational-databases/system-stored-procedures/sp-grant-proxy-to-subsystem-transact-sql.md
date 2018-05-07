---
title: sp_grant_proxy_to_subsystem (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_subsystem_TSQL
- sp_grant_login_to_subsystem
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_proxy_to_subsystem
ms.assetid: 866aaa27-a1e0-453a-9b1b-af39431ad9c2
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a52e19c374c0b1ac14749e1e1bcc53f3a30d2b2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="spgrantproxytosubsystem-transact-sql"></a>sp_grant_proxy_to_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授权代理访问子系统。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_grant_proxy_to_subsystem  
     { [ @proxy_id = ] proxy_id | [ @proxy_name = ] 'proxy_name' },  
     { [ @subsystem_id = ] subsystem_id | [ @subsystem_name = ] 'subsystem_name' }  
```  
  
## <a name="arguments"></a>参数  
 [ **@proxy_id =** ] *id*  
 授予访问权限的代理的代理标识号。 *Proxy_id*是**int**，默认值为 NULL。 任一*proxy_id*或*proxy_name*必须指定，但不能同时指定。  
  
 [ **@proxy_name =** ] **'***proxy_name***'**  
 要授予访问权限的代理的名称。 *Proxy_name*是**sysname**，默认值为 NULL。 任一*proxy_id*或*proxy_name*必须指定，但不能同时指定。  
  
 [ **@subsystem_id =** ] *id*  
 授予访问权限的子系统的 ID 号。 *Subsystem_id*是**int**，默认值为 NULL。 任一*subsystem_id*或*subsystem_name*必须指定，但不能同时指定。 下表列出了每个子系统的值。  
  
|“值”|说明|  
|-----------|-----------------|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX 脚本<br /><br /> **\*\* 重要\* \***  ActiveX 脚本子系统将不再从[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未来版本中的代理[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。|  
|**3**|操作系统 (**CmdExec**)|  
|**4**|复制快照代理|  
|**5**|复制日志读取器代理|  
|**6**|复制分发代理|  
|**7**|复制合并代理|  
|**8**|复制队列读取器代理|  
|**9**|Analysis Services 查询|  
|**10**|Analysis Services 命令|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 包执行|  
|**12**|PowerShell 脚本|  
  
 [ **@subsystem_name =** ] **'***subsystem_name***'**  
 授予访问权限的子系统的名称。 **Subsystem_name**是**sysname**，默认值为 NULL。 任一*subsystem_id*或*subsystem_name*必须指定，但不能同时指定。 下表列出了每个子系统的值。  
  
|“值”|Description|  
|-----------|-----------------|  
|**ActiveScripting**|ActiveX 脚本|  
|**CmdExec**|操作系统 (**CmdExec**)|  
|**快照**|复制快照代理|  
|**LogReader**|复制日志读取器代理|  
|**Distribution**|复制分发代理|  
|**合并**|复制合并代理|  
|**QueueReader**|复制队列读取器代理|  
|**ANALYSISQUERY**|Analysis Services 查询|  
|**ANALYSISCOMMAND**|Analysis Services 命令|  
|**Dts**|SSIS 包执行|  
|**PowerShell**|PowerShell 脚本|  
  
## <a name="remarks"></a>注释  
 授权代理访问子系统将不更改代理中指定的主体服务器的权限。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_grant_proxy_to_subsystem**。  
  
## <a name="examples"></a>示例  
  
### <a name="a-granting-access-to-a-subsystem-by-id"></a>A. 按 ID 授权访问子系统  
 以下示例授权代理 `Catalog application proxy` 访问 ActiveX Scripting 子系统。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_id = 2;  
GO  
```  
  
### <a name="b-granting-access-to-a-subsystem-by-name"></a>B. 按名称授权访问子系统。  
 以下示例授权代理 `Catalog application proxy` 访问 SSIS 包执行子系统。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_proxy_to_subsystem  
    @proxy_name = N'Catalog application proxy',  
    @subsystem_name = N'Dts' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [实现 SQL Server 代理安全性](http://msdn.microsoft.com/library/d770d35c-c8de-4e00-9a85-7d03f45a0f0d)   
 [sp_revoke_proxy_from_subsystem &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-proxy-from-subsystem-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_update_proxy &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-proxy-transact-sql.md)  
  
  
