---
title: sysmail_update_account_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_account_sp
- sysmail_update_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_account_sp
ms.assetid: ba2fdccc-5ed4-40ef-a479-79497b4d61aa
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 68bd628eb791e7af102c6689e22b30ebd5bad73c
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305111"
---
# <a name="sysmail_update_account_sp-transact-sql"></a>sysmail_update_account_sp (Transact-SQL)
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
`[ @account_id = ] account_id` 要更新的帐户 ID。 *account_id*的值为**int**，默认值为 NULL。 必须至少指定*account_id*或*account_name*中的一个。 如果两个都指定，则过程将更改帐户的名称。  
  
`[ @account_name = ] 'account_name'` 要更新的帐户的名称。 *account_name*的值为**sysname**，默认值为 NULL。 必须至少指定*account_id*或*account_name*中的一个。 如果两个都指定，则过程将更改帐户的名称。  
  
`[ @email_address = ] 'email_address'` 要从中发送邮件的新电子邮件地址。 该地址必须是 Internet 电子邮件地址。 该地址中的服务器名称就是数据库邮件用于从该帐户发送邮件的服务器。 *email_address*的值为**nvarchar （128）** ，默认值为 NULL。  
  
`[ @display_name = ] 'display_name'` 要用于从此帐户发送电子邮件的新显示名称。 *display_name*的值为**nvarchar （128）** ，无默认值。  
  
`[ @replyto_address = ] 'replyto_address'` 此帐户发送的电子邮件的答复标头中使用的新地址。 *replyto_address*的值为**nvarchar （128）** ，无默认值。  
  
@no__t 帐户的新说明。 *description*的值为**nvarchar （256）** ，默认值为 NULL。  
  
`[ @mailserver_name = ] 'server_name'` 要用于此帐户的 SMTP 邮件服务器的新名称。 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机必须能够将*server_name*解析为 IP 地址。 *server_name*的值为**sysname**，无默认值。  
  
@no__t 为邮件服务器的新类型。 *server_type*的值为**sysname**，无默认值。 仅支持 **"SMTP"** 值。  
  
`[ @port = ] port_number` 邮件服务器的新端口号。 *port_number*的值为**int**，无默认值。  
  
单个电子邮件的 System.net.mail.smtpclient 的 Timeout 参数 @no__t。 *超时*值**以秒为单位，** 无默认值。  
  
`[ @username = ] 'username'` 使用登录邮件服务器时使用的新用户名。 *用户名*为**sysname**，无默认值。  
  
`[ @password = ] 'password'` 用于登录邮件服务器的新密码。 *密码* 是 **sysname** ，无默认值。  
  
@no__t 指定是否使用 @no__t 1 服务的凭据将邮件发送到 SMTP 服务器。 **use_default_credentials**的值为 bit，无默认值。 当此参数为 1 时，数据库邮件使用[!INCLUDE[ssDE](../../includes/ssde-md.md)]的凭据。 当此参数为0时，数据库邮件使用 **\@username**和 **\@password**在 SMTP 服务器上进行身份验证。 如果 **@no__t 1username**和 **@no__t 3password**为 NULL，则它将使用匿名身份验证。 在指定此参数之前，请洽询您的 SMTP 管理员  
  
@no__t 指定数据库邮件是否使用安全套接字层（SSL）对通信进行加密。 如果 SMTP 服务器需要 SSL，则使用该选项。 **enable_ssl**的值为 bit，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 如果同时指定了帐户名与帐户 ID，则存储过程不仅会更新帐户信息，还会更改帐户名。 更改帐户名可能有助于纠正帐户名中的错误。  
  
 存储过程**sysmail_update_account_sp**位于**msdb**数据库中，由**dbo**架构拥有。 如果当前数据库不是**msdb**，则必须使用由三部分组成的名称来执行该过程。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-information-for-an-account"></a>A. 更改帐户的信息  
 下面的示例在**msdb**数据库中更新帐户 `AdventureWorks Administrator`。 此帐户的信息被设置为提供的值。  
  
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
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件存储过程&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
