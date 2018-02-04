---
title: "sysmail_update_account_sp (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4be8c0c87771f89d92cc0344c207149467c4554c
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailupdateaccountsp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改现有数据库邮件帐户中的信息。  
 
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_update_account_sp [ [ @account_id = ] account_id ] [ , ] [ [ @account_name = ] 'account_name' ] ,  
    [ @email_address = ] 'email_address' ,   
    [ @display_name = ] 'display_name' ,   
    [ @replyto_address = ] 'replyto_address' ,  
    [ @description = ] 'description' ,   
    [ @mailserver_name = ] 'server_name' ,   
    [ @mailserver_type = ] 'server_type' ,   
    [ @port = ] port_number ,   
    [ @timeout = ] 'timeout' ,  
    [ @username = ] 'username' ,  
    [ @password = ] 'password' ,  
    [ @use_default_credentials = ] use_default_credentials ,  
    [ @enable_ssl = ] enable_ssl   
```  
  
## <a name="arguments"></a>参数  
 [ **@account_id** = ] *account_id*  
 要更新的帐户 ID。 *account_id*是**int**，默认值为 NULL。 至少一个*account_id*或*account_name*必须指定。 如果两个都指定，则过程将更改帐户的名称。  
  
 [ **@account_name** = ] **'***account_name***'**  
 要更新的帐户名。 *account_name*是**sysname**，默认值为 NULL。 至少一个*account_id*或*account_name*必须指定。 如果两个都指定，则过程将更改帐户的名称。  
  
 [ **@email_address** = ] **'***email_address***'**  
 发件人的新电子邮件地址。 该地址必须是 Internet 电子邮件地址。 该地址中的服务器名称就是数据库邮件用于从该帐户发送邮件的服务器。 *电子邮件地址*是**nvarchar （128)**，默认值为 NULL。  
  
 [ **@display_name** = ] **'***display_name***'**  
 从该帐户发出的电子邮件中使用的新显示名称。 *display_name*是**nvarchar （128)**，无默认值。  
  
 [ **@replyto_address** = ] **'***replyto_address***'**  
 从该帐户发出的电子邮件的答复标题中使用的新地址。 *replyto_address*是**nvarchar （128)**，无默认值。  
  
 [ **@description** = ] **'***description***'**  
 对帐户的新说明。 *说明*是**nvarchar(256)**，默认值为 NULL。  
  
 [ **@mailserver_name** = ] **'***server_name***'**  
 该帐户要使用的 SMTP 邮件服务器的新名称。 运行的计算机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须能够解析*server_name*为 IP 地址。 *server_name*是**sysname**，无默认值。  
  
 [ **@mailserver_type** = ] **'***server_type***'**  
 邮件服务器的新类型。 *server_type*是**sysname**，无默认值。 只有值**SMTP**支持。  
  
 [ **@port** = ] *port_number*  
 邮件服务器的新端口号。 *port_number*是**int**，无默认值。  
  
 [ **@timeout** = ] **'***timeout***'**  
 单个电子邮件信息的 SmtpClient.Send 的超时参数。 *超时*是**int**以秒为单位，无默认值。  
  
 [ **@username** = ] **'***username***'**  
 登录到邮件服务器时使用的新用户名。 *用户名称*是**sysname**，无默认值。  
  
 [ **@password** = ] **'***password***'**  
 登录到邮件服务器时使用的新密码。 *密码*是**sysname**，无默认值。  
  
 [ **@use_default_credentials** = ] use_default_credentials  
 指定是否使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]服务的凭据将邮件发送到 SMTP 服务器。 **use_default_credentials**位，无默认值。 当此参数为 1 时，数据库邮件使用[!INCLUDE[ssDE](../../includes/ssde-md.md)]的凭据。 此参数为 0 时，数据库邮件使用 **@username** 和 **@password**  SMTP 服务器上进行身份验证。 如果 **@username** 和 **@password** 均为 NULL，则它将使用匿名身份验证。 在指定此参数之前，请洽询您的 SMTP 管理员  
  
 [ **@enable_ssl** = ] enable_ssl  
 指定数据库邮件是否使用安全套接字层 (SSL) 对通信进行加密。 如果 SMTP 服务器需要 SSL，则使用该选项。 **enable_ssl**位，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 如果同时指定了帐户名与帐户 ID，则存储过程不仅会更新帐户信息，还会更改帐户名。 更改帐户名可能有助于纠正帐户名中的错误。  
  
 存储的过程**sysmail_update_account_sp**处于**msdb**数据库，而且由拥有**dbo**架构。 如果当前数据库不是，必须使用由三部分名称执行过程**msdb**。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-information-for-an-account"></a>A. 更改帐户的信息  
 下面的示例更新帐户`AdventureWorks Administrator`中**msdb**数据库。 此帐户的信息被设置为提供的值。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_name = 'AdventureWorks Administrator'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
### <a name="b-changing-the-name-of-an-account-and-the-information-for-an-account"></a>B. 更改帐户名和帐户信息  
 下面的示例更改了帐户 ID 为 `125` 的帐户名并更新了帐户信息。 此帐户的新名称为 `Backup Mail Server`。  
  
```  
EXECUTE msdb.dbo.sysmail_update_account_sp  
     @account_id = 125  
    ,@account_name = 'Backup Mail Server'  
    ,@description = 'Mail account for administrative e-mail.'  
    ,@email_address = 'dba@Adventure-Works.com'  
    ,@display_name = 'AdventureWorks Automated Mailer'  
    ,@replyto_address = NULL  
    ,@mailserver_name = 'smtp-backup.Adventure-Works.com'  
    ,@mailserver_type = 'SMTP'  
    ,@port = 25  
    ,@timeout = 60  
    ,@username = NULL  
    ,@password = NULL  
    ,@use_default_credentials = 0  
    ,@enable_ssl = 0;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
