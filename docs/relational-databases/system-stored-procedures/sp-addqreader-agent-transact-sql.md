---
title: sp_addqreader_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addqreader_agent_TSQL
- sp_addqreader_agent
helpviewer_keywords:
- sp_addqreader_agent
ms.assetid: dc9f591a-e67e-4ba8-bf47-defd5eda0822
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6700e0d060e426fef09e8db118b373d7919175a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830395"
---
# <a name="spaddqreaderagent-transact-sql"></a>sp_addqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为给定分发服务器添加队列读取器代理。 此存储过程在分发服务器上针对分发数据库执行，或在发布服务器上针对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addqreader_agent [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
    [ , [ @job_name = ] 'job_name'  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>参数  
 [ **@job_login**=] **'***job_login*****  
 用于运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 帐户的登录名。 *job_login*是**nvarchar(257)**，无默认值。 此 Windows 帐户总是用于与分发服务器建立代理连接。  
  
 [ **@job_password**=] **'***job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为保证安全性，应当在运行时再提供登录名和密码。  
  
 [ **@job_name**=] **'***job_name*****  
 现有代理作业的名称。 *job_name*是**sysname**，默认值为 NULL。 只有在使用现有作业而不是新创建作业（默认值）创建代理时，才需要指定此参数。  
  
 [  **@frompublisher=** ] *frompublisher*  
 指定在发布服务器是否正在执行该过程。 *frompublisher*为 bit，默认值为**0**。 值为**1**意味着正在从发布服务器上，对发布数据库执行该过程。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_addqreader_agent**事务复制中使用。  
  
 **sp_addqreader_agent**必须在支持排队更新后的分发服务器上的至少一次执行[sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)之前[sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。  
  
 在执行时，会取消该队列读取器代理作业[sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_addqreader_agent**。  
  
## <a name="see-also"></a>请参阅  
 [允许更新事务发布的订阅](../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [升级复制脚本（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [Updatable Subscriptions for Transactional Replication](../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [sp_changeqreader_agent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md)   
 [sp_helpqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)  
  
  
