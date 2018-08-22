---
title: sp_revoke_proxy_from_subsystem (TRANSACT-SQL) |Microsoft Docs
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
- sp_revoke_login_from_subsystem
- sp_revoke_login_from_subsystem_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_revoke_proxy_from_subsystem
ms.assetid: b87bc8ba-3ea8-4aed-b54b-32c3d82d9d2a
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c19e54fe6f9d9280d19ab6861cf27ffa20df636
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392735"
---
# <a name="sprevokeproxyfromsubsystem-transact-sql"></a>sp_revoke_proxy_from_subsystem (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  撤消代理对子系统的访问权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_revoke_proxy_from_subsystem   
    [ @proxy_id = ] proxy_id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @subsystem_id = ] subsystem_id,  
    [ @subsystem_name = ] 'subsystem_name'  
```  
  
## <a name="arguments"></a>参数  
 [ **@proxy_id** = ] *id*  
 要撤消访问权限的代理的代理标识号。 *Proxy_id*是**int**，默认值为 NULL。 任一*proxy_id*或*proxy_name*必须指定，但不能同时指定两者。  
  
 [ **@proxy_name** = ] **'***proxy_name***'**  
 要撤消访问权限的代理的名称。 *Proxy_name*是**sysname**，默认值为 NULL。 任一*proxy_id*或*proxy_name*必须指定，但不能同时指定两者。  
  
 [ **@subsystem_id** = ] *id*  
 要撤消对其访问权限的子系统的 id 号。 *Subsystem_id*是**int**，默认值为 NULL。 任一*subsystem_id*或*subsystem_name*必须指定，但不能同时指定两者。 下表列出了每个子系统的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**2**|ActiveX 脚本<br /><br /> **\*\* 重要\* \*** 将删除 ActiveX 脚本编写子系统[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的未来版本中的代理[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。|  
|**3**|操作系统 (CmdExec)|  
|**4**|复制快照代理|  
|**5**|复制日志读取器代理|  
|**6**|复制分发代理|  
|**7**|Replication Merge Agent|  
|**8**|复制队列读取器代理|  
|**9**|Analysis Services 命令|  
|**10**|Analysis Services 查询|  
|**11**|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 包执行|  
|**12**|PowerShell 脚本|  
  
 [ **@subsystem_name**= ] **'***subsystem_name***'**  
 要撤消对其访问权限的子系统的名称。 *Subsystem_name*是**sysname**，默认值为 NULL。 任一*subsystem_id*或*subsystem_name*必须指定，但不能同时指定两者。 下表列出了每个子系统的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|ActiveScripting|ActiveX 脚本|  
|CmdExec|操作系统 (CmdExec)|  
|快照|复制快照代理|  
|LogReader|复制日志读取器代理|  
|Distribution|复制分发代理|  
|合并|Replication Merge Agent|  
|QueueReader|复制队列读取器代理|  
|ANALYSISQUERY|Analysis Services 命令|  
|ANALYSISCOMMAND|Analysis Services 查询|  
|Dts|[!INCLUDE[ssIS](../../includes/ssis-md.md)] 包执行|  
|PowerShell|PowerShell 脚本|  
  
## <a name="remarks"></a>Remarks  
 撤消对子系统的访问权限不会更改代理中指定的主体数据库的权限。  
  
> [!NOTE]  
>  若要确定哪些作业步骤引用了代理，请右键单击**代理**节点下的**SQL Server 代理**在 Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]，然后单击**属性**。 在中**代理帐户属性**对话框中，选择**引用**页后，可以查看引用此代理的所有作业步骤。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_revoke_proxy_from_subsystem**。  
  
## <a name="examples"></a>示例  
 以下示例撤消代理 `Catalog application proxy` 对 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 子系统的访问权限。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_proxy_from_subsystem  
    @proxy_name = 'Catalog application proxy',  
    @subsystem_name = N'Dts';  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [实现 SQL Server 代理安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_grant_proxy_to_subsystem &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-proxy-to-subsystem-transact-sql.md)  
  
  
