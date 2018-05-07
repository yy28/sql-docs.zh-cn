---
title: sysmail_add_account_sp (Transact SQL) |Microsoft 文档
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
- sysmail_add_account_sp
- sysmail_add_account_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_account_sp
ms.assetid: 65e15e2e-107c-49c3-b12c-f4edf0eb1617
caps.latest.revision: 40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eab3408b20a7c144ba68d57ceba8d4acf3e54f15
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
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
 [ **@account_name** = ] **'***account_name***'**  
 要添加的帐户的名称。 *account_name*是**sysname**，无默认值。  
  
 [ **@email_address** = ] **'***email_address***'**  
 要将从消息发送的电子邮件地址。 该地址必须是 Internet 电子邮件地址。 *电子邮件地址*是**nvarchar （128)**，无默认值。 例如，帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可能会发送电子邮件发件人地址**SqlAgent@Adventure-Works.com**。  
  
 [ **@display_name** =] *****display_name*****  
 在从该帐户发出的电子邮件中使用的显示名称。 *display_name*是**nvarchar （128)**，默认值为 NULL。 例如，帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可能会显示名称**SQL Server Agent Automated Mailer**上电子邮件。  
  
 [ **@replyto_address** =] *****replyto_address*****  
 对于来自此帐户的邮件发送答复的地址。 *replyto_address*是**nvarchar （128)**，默认值为 NULL。 例如，回复的帐户[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理可能会发送给数据库管理员**danw@Adventure-Works.com**。  
  
 [ **@description** = ] **'***description***'**  
 帐户说明。 *说明*是**nvarchar(256)**，默认值为 NULL。  
  
 [ **@mailserver_name** = ] **'***server_name***'**  
 此帐户所用 SMTP 邮件服务器的名称或 IP 地址。 运行的计算机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]必须能够解析*server_name*为 IP 地址。 *server_name*是**sysname**，无默认值。  
  
 [ **@mailserver_type** = ] '*server_type*'  
 电子邮件服务器的类型。 *server_type*是**sysname**，默认值为**SMTP**...  
  
 [ **@port** = ] *port_number*  
 电子邮件服务器端口号。 *port_number*是**int**，默认值为 25。  
  
 [ **@username** =] *****用户名*****  
 用于登录到电子邮件服务器的用户名。 *用户名*是**nvarchar （128)**，默认值为 NULL。 如果此参数为 NULL，则数据库电子邮件不对此帐户进行身份验证。 如果邮件服务器不要求身份验证，则使用 NULL 作为用户名。  
  
 [ **@password** =] *****密码*****  
 用于登录电子邮件服务器的密码。 *密码*是**nvarchar （128)**，默认值为 NULL。 除非指定了用户名，否则无需提供密码。  
  
 [ **@use_default_credentials** =] use_default_credentials  
 指定是否使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的凭据将邮件发送到 SMTP 服务器。 **use_default_credentials**位，默认值为 0。 当此参数为 1 时，数据库邮件使用[!INCLUDE[ssDE](../../includes/ssde-md.md)]的凭据。 当此参数为 0 时，数据库邮件将发送**@username**和**@password**参数，如果存在，否则会发送邮件，而无需**@username**和**@password**参数。  
  
 [ **@enable_ssl** =] enable_ssl  
 指定数据库邮件是否使用安全套接字层对通信进行加密。 **Enable_ssl**位，默认值为 0。  
  
 [ **@account_id** =] *account_id*输出  
 返回新帐户的帐户 ID。 *account_id*是**int**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 数据库邮件提供单独的参数**@email_address**， **@display_name**，和**@replyto_address**。 **@email_address**参数是从其发送消息的地址。 **@display_name**参数是中显示的名称**从：**字段的电子邮件。 **@replyto_address**参数是地址回复电子邮件将发送到的位置。 例如，用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的帐户可以从仅用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的电子邮件地址发送电子邮件。 来自该地址的邮件应显示友好名称，以便收件人可以轻松确定是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理发来的邮件。 如果收件人回复该邮件，则回复应发送给数据库管理员，而不是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理使用的地址。 对于此方案，此帐户使用**SqlAgent@Adventure-Works.com**作为电子邮件地址。 显示名称设置为**SQL Server Agent Automated Mailer**。 此帐户使用**danw@Adventure-Works.com**作为对地址的答复，因此对此帐户发送的邮件回复转到数据库管理员，而不是的电子邮件地址[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理。 通过为上述三个参数提供独立的设置，数据库邮件允许您配置邮件来适应您的需求。  
  
 **@mailserver_type**参数支持值**SMTP**。  
  
 当**@use_default_credentials**是 1 邮件发送到 SMTP 服务器使用的凭据[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]。 当**@use_default_credentials**为 0 和**@username**和**@password**指定的帐户，此帐户使用 SMTP 身份验证。 **@username**和**@password**是为 SMTP 服务器，不凭据时使用的帐户的凭据[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或计算机的网络。  
  
 存储的过程**sysmail_add_account_sp**处于**msdb**数据库，而且由拥有**dbo**架构。 如果当前数据库不是，必须使用由三部分名称执行过程**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认为成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将创建一个名为 `AdventureWorks Administrator` 的帐户。 此帐户使用电子邮件地址 `dba@Adventure-Works.com`，并将邮件发送到 SMTP 邮件服务器 `smtp.Adventure-Works.com`。 此帐户显示发送电子邮件`AdventureWorks Automated Mailer`上**从：**邮件的行。 对此邮件的回复将发往 `danw@Adventure-Works.com`。  
  
```  
EXECUTE msdb.dbo.sysmail_add_account_sp  
    @account_name = 'AdventureWorks Administrator',  
    @description = 'Mail account for administrative e-mail.',  
    @email_address = 'dba@Adventure-Works.com',  
    @display_name = 'AdventureWorks Automated Mailer',  
    @mailserver_name = 'smtp.Adventure-Works.com' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
