---
title: "sp_changelogreader_agent (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_changelogreader_agent
- sp_changelogreader_agent_TSQL
helpviewer_keywords: sp_changelogreader_agent
ms.assetid: 929b2fa7-1267-41d0-8b69-e9ab26a62c0f
caps.latest.revision: "21"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 42668e8b915af31cf746800fc65312caf84ad88e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spchangelogreaderagent-transact-sql"></a>sp_changelogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改日志读取器代理的安全属性。 在发布服务器的发布数据库上执行此存储的过程。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changelogreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@job_login** =] *job_login*  
 用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)**，默认值为 NULL。 *这不能更改为非*[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *发布服务器。*  
  
 [  **@job_password** =] *job_password*  
 用于运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的密码。 *job_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [  **@publisher_security_mode** =] *publisher_security_mode*  
 连接到发布服务器时代理所使用的安全模式。 *publisher_security_mode*是**smallint**，默认值为 NULL。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，和**1**指定 Windows 身份验证。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [  **@publisher_login** =] *publisher_login*  
 连接到发布服务器时所使用的登录名。 *publisher_login*是**sysname**，默认值为 NULL。 *publisher_login*时，必须指定*publisher_security_mode*是**0**。 如果*publisher_login*为 NULL 和*publisher_security_mode*是**1**，然后中指定的 Windows 帐户*job_login*时使用连接到发布服务器。  
  
 [  **@publisher_password** =] *publisher_password*  
 连接到发布服务器时所使用的密码。 *publisher_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [  **@publisher** =] *发布服务器*  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 仅非 SQL Server 发布服务器支持此参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_changelogreader_agent**事务复制中使用。  
  
 **sp_changelogreader_agent**用于更改运行日志读取器代理的 Windows 帐户。 可以更改现有 Windows 登录名的密码，或提供新的 Windows 登录名和密码。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_changelogreader_agent**。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_helplogreader_agent &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md)   
 [sp_addlogreader_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
  
