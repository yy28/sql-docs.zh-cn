---
title: sp_changeqreader_agent (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changeqreader_agent_TSQL
- sp_changeqreader_agent
helpviewer_keywords:
- sp_changeqreader_agent
ms.assetid: d3fe79c5-31ef-4565-bf38-b476b5fb16f7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 21da0ca61d2d9075fe7c962156443fd85f3ebefd
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135119"
---
# <a name="spchangeqreaderagent-transact-sql"></a>sp_changeqreader_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改队列读取器代理的安全属性。 此存储过程在分发服务器上针对分发数据库执行，或在发布服务器上针对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changeqreader_agent [ [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @frompublisher = ] frompublisher   
```  
  
## <a name="arguments"></a>参数  
 [ **@job_login**=] **'**_job_login_  
 用于运行代理的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 帐户的登录名。 *job_login*是**nvarchar(257)**，默认值为 NULL。  
  
 [ **@job_password**=] **'**_job_password_  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，默认值为 NULL。  
  
 [  **@frompublisher=** ] *frompublisher*  
 指定是否在发布服务器上执行该过程。 *frompublisher*为 bit，默认值为**0**。 值为**1**意味着正在从发布服务器上，对发布数据库执行该过程。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changeqreader_agent**事务复制中使用。  
  
 **sp_changeqreader_agent**用于更改运行队列读取器代理的 Windows 帐户。 可以更改现有 Windows 登录名的密码，或提供新的 Windows 登录名和密码。  
  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_changeqreader_agent**。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改复制安全设置](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)   
 [sp_addqreader_agent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
  
