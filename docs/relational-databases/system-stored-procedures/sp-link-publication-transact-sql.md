---
title: sp_link_publication (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_link_publication_TSQL
- sp_link_publication
helpviewer_keywords:
- sp_link_publication
ms.assetid: 1945ed24-f9f1-4af6-94ca-16d8e864706e
caps.latest.revision: 41
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 17e1b051fed32e78cd18cc634b7688245ecb0972
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "33001924"
---
# <a name="splinkpublication-transact-sql"></a>sp_link_publication (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置在连接到发布服务器时立即更新订阅的同步触发器所使用的配置和安全信息。 此存储过程在订阅服务器的订阅数据库中执行。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
> [!IMPORTANT]  
>  在某些情况下，如果订阅服务器正在运行此存储的过程可以失败[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 或更高版本和发布服务器上运行的是早期版本。 如果存储过程在上述情况下失败，请将发布服务器升级至 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 1 或更高版本。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_link_publication [ @publisher = ] 'publisher'   
        , [ @publisher_db = ] 'publisher_db'   
        , [ @publication = ] 'publication'   
        , [ @security_mode = ] security_mode  
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ]'password' ]  
    [ , [ @distributor = ] 'distributor' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher**=] *****发布服务器*****  
 要链接到的发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [ **@publisher_db**=] *****publisher_db*****  
 要链接到的发布服务器数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication**=] *****发布*****  
 要链接到的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@security_mode**=] *security_mode*  
 订阅服务器为执行立即更新而连接到远程发布服务器时所用的安全模式。 *security_mode*是**int**，并且可以为这些值之一。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
|“值”|说明|  
|-----------|-----------------|  
|**0**|使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用为此存储过程中指定的登录名的身份验证*登录*和*密码*。<br /><br /> 注意： 在以前版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，此选项用于指定动态远程过程调用 (RPC)。|  
|**1**|使用在订阅服务器上进行更改的用户的安全上下文（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证或 Windows 身份验证）。<br /><br /> 注意： 此帐户必须也存在在具有足够的特权的发布者。 使用 Windows 身份验证时，必须支持安全策略帐户委托。|  
|**2**|使用现有的、 用户定义链接的服务器登录名创建使用**sp_link_publication**。|  
  
 [ **@login**=] *****登录*****  
 登录。 login 的数据类型为 sysname，默认值为 NULL。 此参数必须是时指定*security_mode*是**0**。  
  
 [ **@password**=] *****密码*****  
 是的密码。 *密码*是**sysname**，默认值为 NULL。 此参数必须是时指定*security_mode*是**0**。  
  
 [  **@distributor=** ] *****分发服务器*****  
 是分发服务器的名称。 *分发服务器*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_link_publication**立即更新订阅事务复制中使用。  
  
 **sp_link_publication**可以用于推送和请求订阅。 在创建订阅之前或之后都可以调用此过程。 插入或更新一个条目[MSsubscription_properties &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)系统表。  
  
 对于推送订阅，该条目可以通过可清除[sp_subscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)。 对于请求订阅，该条目可以通过可清除[sp_droppullsubscription &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)或[sp_subscription_cleanup &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)。 你还可以调用**sp_link_publication**使用空密码，以清除中的条目[MSsubscription_properties &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)有关安全问题的系统表。  
  
 当立即更新订阅服务器连接到发布服务器时，它使用的默认模式不允许使用 Windows 身份验证进行连接。 若要用 Windows 身份验证模式进行连接，则必须设置到发布服务器的链接服务器，且立即更新订阅服务器在更新订阅服务器时应使用该连接。 这要求**sp_link_publication**使用运行*security_mode* = **2**。 使用 Windows 身份验证时，必须支持安全策略帐户委托。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent_failover](../../relational-databases/replication/codesnippet/tsql/sp-link-publication-tran_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_link_publication**。  
  
## <a name="see-also"></a>另请参阅  
 [sp_droppullsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [sp_subscription_cleanup &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
