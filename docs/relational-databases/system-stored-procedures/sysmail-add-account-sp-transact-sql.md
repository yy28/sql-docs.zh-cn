---
title: sysmail_add_account_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
author: stevestein
ms.author: sstein
ms.openlocfilehash: 6f09f54a4b5869279cfa3c53c5e82d86213736f0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68017846"
---
# <a name="sysmailaddaccountsp-transact-sql"></a>sysmail_add_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建一个新的数据库邮件帐户，用于保存有关 SMTP 帐户的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_add_account_sp  [ @account_name = ] 'account_name',  
    [ @email_address = ] 'email_address' ,  
    [ [ @display_name = ] 'display_name' , ]  
    [ [ @replyto_address = ] 'replyto_address' , ]  
    [ [ @description = ] 'description' , ]  
    [ @mailserver_name = ] 'server_name'   
    [ , [ @mailserver_type = ] 'server_type' ]  
    [ , [ @port = ] port_number ]  
    [ , [ @username = ] 'username' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @use_default_credentials = ] use_default_credentials ]  
    [ , [ @enable_ssl = ] enable_ssl ]  
    [ , [ @account_id = ] account_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
`[ @account_name = ] 'account_name'` 要添加的帐户的名称。 *account_name*是**sysname**，无默认值。  
  
`[ @email_address = ] 'email_address'` 要从其发送消息的电子邮件地址。 该地址必须是 Internet 电子邮件地址。 *email_address*是**nvarchar （128)** ，无默认值。 例如，为帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可能会发送电子邮件发件人地址 **SqlAgent@Adventure-Works.com** 。  
  
`[ @display_name = ] 'display_name'` 要从该帐户的电子邮件上使用的显示名称。 *display_name*是**nvarchar （128)** ，默认值为 NULL。 例如，为帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可能会显示名称**SQL Server Agent Automated Mailer**发出的电子邮件。  
  
`[ @replyto_address = ] 'replyto_address'` 此帐户从响应消息发送到的地址。 *replyto_address*是**nvarchar （128)** ，默认值为 NULL。 例如，给的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可能会发送给数据库管理员 **danw@Adventure-Works.com** 。  
  
`[ @description = ] 'description'` 是帐户的说明。 *描述*是**nvarchar(256)** ，默认值为 NULL。  
  
`[ @mailserver_name = ] 'server_name'` 名称或要用于此帐户的 SMTP 邮件服务器的 IP 地址。 运行的计算机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须能够解析*server_name*为 IP 地址。 *server_name*是**sysname**，无默认值。  
  
`[ @mailserver_type = ] 'server_type'` 电子邮件服务器的类型。 *server_type*是**sysname**，默认值为 **'SMTP'** ...  
  
`[ @port = ] port_number` 电子邮件服务器端口号。 *port_number*是**int**，默认值为 25。  
  
`[ @username = ] 'username'` 要用于登录到电子邮件服务器上的用户名称。 *用户名*是**nvarchar （128)** ，默认值为 NULL。 如果此参数为 NULL，则数据库电子邮件不对此帐户进行身份验证。 如果邮件服务器不要求身份验证，则使用 NULL 作为用户名。  
  
`[ @password = ] 'password'` 要用于登录到电子邮件服务器上的密码。 *密码*是**nvarchar （128)** ，默认值为 NULL。 除非指定了用户名，否则无需提供密码。  
  
`[ @use_default_credentials = ] use_default_credentials` 指定是否将邮件发送到 SMTP 服务器使用的凭据[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 **use_default_credentials**为 bit，默认值为 0。 当此参数为 1 时，数据库邮件使用[!INCLUDE[ssDE](../../includes/ssde-md.md)]的凭据。 当此参数为 0 时，数据库邮件将发送 **@username** 并 **@password** 参数，如果存在，否则将发送邮件，而无需 **@username** 并 **@password** 参数。  
  
`[ @enable_ssl = ] enable_ssl` 指定数据库邮件是否对使用安全套接字层的通信进行加密。 **Enable_ssl**为 bit，默认值为 0。  
  
`[ @account_id = ] account_id OUTPUT` 返回新的帐户的帐户 id。 *account_id*是**int**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 数据库邮件提供单独的参数 **@email_address** ， **@display_name** ，以及 **@replyto_address** 。 **@email_address** 参数是从其发送消息的地址。 **@display_name** 参数是名称中所示**从：** 字段的电子邮件。 **@replyto_address** 参数是地址发送到电子邮件的回复。 例如，用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的帐户可以从仅用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的电子邮件地址发送电子邮件。 来自该地址的邮件应显示友好名称，以便收件人可以轻松确定是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理发来的邮件。 如果收件人回复该邮件，则回复应发送给数据库管理员，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理使用的地址。 对于此方案，该帐户将使用 **SqlAgent@Adventure-Works.com** 作为电子邮件地址。 显示名称设置为**SQL Server Agent Automated Mailer**。 该帐户将使用 **danw@Adventure-Works.com** 作为回复地址，因此对此帐户发送的邮件的答复转到数据库管理员而不是电子邮件地址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。 通过为上述三个参数提供独立的设置，数据库邮件允许您配置邮件来适应您的需求。  
  
 **@mailserver_type** 参数支持值 **'SMTP'** 。  
  
 当 **@use_default_credentials** 是 1 时，邮件发送到 SMTP 服务器使用的凭据[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 当 **@use_default_credentials** 为 0 和一个 **@username** 并 **@password** 指定帐户，该帐户将使用 SMTP 身份验证。 **@username** 并 **@password** 是帐户使用的 SMTP 服务器，而不是凭据的凭据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或计算机的网络。  
  
 存储的过程**sysmail_add_account_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将创建一个名为 `AdventureWorks Administrator` 的帐户。 此帐户使用电子邮件地址 `dba@Adventure-Works.com`，并将邮件发送到 SMTP 邮件服务器 `smtp.Adventure-Works.com`。 此帐户显示发送电子邮件`AdventureWorks Automated Mailer`上**从：** 消息行。 对此邮件的回复将发往 `danw@Adventure-Works.com`。  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
