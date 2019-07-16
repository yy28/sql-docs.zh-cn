---
title: sp_addlogreader_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addlogreader_agent
- sp_addlogreader_agent_TSQL
helpviewer_keywords:
- sp_addlogreader_agent
ms.assetid: d83096b9-96ee-4789-bde0-940d4765b9ed
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 062561d440a276fccf5310731db7503e67f7f43e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68118098"
---
# <a name="spaddlogreaderagent-transact-sql"></a>sp_addlogreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为给定数据库添加日志读取器代理。 在发布服务器上对发布数据库执行此存储的过程。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addlogreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @job_login = ] 'job_login'` 登录名[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 帐户下运行的代理。 *job_login*是**nvarchar(257)** ，默认值为 NULL。 此 Windows 帐户总是用于与分发服务器建立代理连接。  
  
> [!NOTE]
>  对于非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，这必须是相同的登录名中指定[sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)。  
  
`[ @job_password = ] 'job_password'` 是用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为保证安全性，应当在运行时再提供登录名和密码。  
  
`[ @job_name = ] 'job_name'` 是现有的代理作业的名称。 *job_name*是**sysname**，默认值为 NULL。 只有在使用现有作业而不是使用新创建的作业（默认值）来启动代理时，才需要指定此参数。  
  
`[ @publisher_security_mode = ] publisher_security_mode` 安全模式使用代理连接到发布服务器时。 *publisher_security_mode*是**smallint**，默认值为**1**。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，并**1**指定 Windows 身份验证。 值为**0**必须为指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
`[ @publisher_login = ] 'publisher_login'` 是连接到发布服务器时使用的登录名。 *publisher_login*是**sysname**，默认值为 NULL。 *publisher_login*时，必须指定*publisher_security_mode*是**0**。 如果*publisher_login*为 NULL 并*publisher_security_mode*是**1**，然后在指定的 Windows 帐户*job_login*将使用当连接到发布服务器。  
  
`[ @publisher_password = ] 'publisher_password'` 连接到发布服务器时使用的密码。 *publisher_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为保证安全性，应当在运行时再提供登录名和密码。  
  
`[ @publisher = ] 'publisher'` 是的名称的非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器，无需指定此参数。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addlogreader_agent**事务复制中使用。  
  
 必须执行**sp_addlogreader_agent**以添加日志读取器代理，如果升级的数据库，以便将复制到此版本的已启用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用数据库创建的发布之前。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addlogreader_agent**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addlogreader-agent-tr_1.sql)]  
  
## <a name="see-also"></a>请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changelogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
