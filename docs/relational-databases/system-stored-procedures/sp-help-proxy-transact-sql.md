---
title: sp_help_proxy (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_proxy
- sp_help_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_proxy
ms.assetid: a2fce164-2b64-40c2-8f35-6eeb7844abf1
caps.latest.revision: 38
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f7053bfc6ccbca71783d0bbcdb8b9b5544f9d20
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpproxy-transact-sql"></a>sp_help_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出一个或多个代理的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @subsystem_name = ] 'subsystem_name' ,  
    [ @name = ] 'name'  
```  
  
## <a name="arguments"></a>参数  
 [ **@proxy_id** = ] *id*  
 要列出信息的代理的代理标识号。 *Proxy_id*是**int**，默认值为 NULL。 任一*id*或*proxy_name*可指定。  
  
 [ **@proxy_name** = ] **'***proxy_name***'**  
 要列出信息的代理的名称。 *Proxy_name*是**sysname**，默认值为 NULL。 任一*id*或*proxy_name*可指定。  
  
 [ **@subsystem_name** =] '*subsystem_name*  
 要列出代理的子系统名称。 *Subsystem_name*是**sysname**，默认值为 NULL。 当*subsystem_name*指定，则*名称*还必须指定。  
  
 下表列出了每个子系统的值。  
  
|“值”|Description|  
|-----------|-----------------|  
|ActiveScripting|ActiveX 脚本|  
|CmdExec|操作系统 (CmdExec)|  
|快照|复制快照代理|  
|LogReader|复制日志读取器代理|  
|Distribution|复制分发代理|  
|合并|复制合并代理|  
|QueueReader|复制队列读取器代理|  
|ANALYSISQUERY|Analysis Services 命令|  
|ANALYSISCOMMAND|Analysis Services 查询|  
|Dts|SSIS 包执行|  
|PowerShell|PowerShell 脚本|  
  
 [ **@name** =] '*名称*  
 要为其列出代理的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的名称。 名称是**nvarchar(256)**，默认值为 NULL。 当*名称*指定，则*subsystem_name*还必须指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|代理服务器标识号。|  
|**名称**|**sysname**|代理服务器的名称。|  
|**credential_identity**|**sysname**|与代理关联的凭据的 Microsoft Windows 域名和用户名。|  
|**enabled**|**tinyint**|是否启用了此代理。 { **0** = 不启用， **1** = 启用}|  
|**说明**|**nvarchar(1024)**|对此代理的说明。|  
|**user_sid**|**varbinary(85)**|此代理的 Windows 用户的 Windows 安全 ID。|  
|**credential_id**|**int**|与此代理关联的凭据的标识符。|  
|**credential_identity_exists**|**int**|是否存在 credential_identity。 { 0 = 不存在，1 = 存在 }|  
  
## <a name="remarks"></a>注释  
 当未提供参数时， **sp_help_proxy**列出实例中的所有代理的信息。  
  
 若要确定的登录名的代理可用于给定子系统，指定*名称*和*subsystem_name*。 这些自变量提供时， **sp_help_proxy**列出该登录名指定可以访问并且可能使用来指定子系统的代理。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有 **sysadmin** 固定服务器角色的成员才可以执行此存储过程。 其他用户必须被授予 **msdb** 数据库中的 **SQLAgentOperatorRole** 固定数据库角色的权限。  
  
 有关详细信息**SQLAgentOperatorRole**，请参阅[SQL Server Agent Fixed Database Roles](http://msdn.microsoft.com/library/719ce56b-d6b2-414a-88a8-f43b725ebc79)。  
  
> [!NOTE]  
>  **Credential_identity**和**user_sid**列仅返回结果集时的成员**sysadmin**执行此存储的过程。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-information-for-all-proxies"></a>A. 列出所有代理的信息  
 以下示例将列出实例中所有代理的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy ;  
GO  
```  
  
### <a name="b-listing-information-for-a-specific-proxy"></a>B. 列出指定代理的信息  
 以下示例将列出名为 `Catalog application proxy` 的代理的信息。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)  
  
  
