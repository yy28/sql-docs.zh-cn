---
title: "sysmail_help_account_sp (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- sysmail_help_account_sp_TSQL
- sysmail_help_account_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_account_sp
ms.assetid: 87c7c39c-8e05-4e68-9272-45f908809c3b
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b811fef9f1c2a89590e1e03f4fbe1b214ddc902d
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysmailhelpaccountsp-transact-sql"></a>sysmail_help_account_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出有关数据库邮件帐户的信息（密码除外）。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_account_sp [ [ @account_id = ] account_id | [ @account_name = ] 'account_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@account_id** = ] *account_id*  
 列出其帐户信息的帐户的 ID。 *account_id*是**int**，默认值为 NULL。  
  
 [ **@account_name** = ] **'***account_name***'**  
 列出其帐户信息的帐户的名称。 *account_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 返回包含下面列出的列的结果集。  
  
||||  
|-|-|-|  
|列名|数据类型|Description|  
|**account_id**|**int**|帐户 ID。|  
|**名称**|**sysname**|帐户名称。|  
|**说明**|**nvarchar(256)**|对帐户的说明。|  
|**email_address**|**nvarchar(128)**|发送消息的电子邮件地址。|  
|**display_name**|**nvarchar(128)**|帐户的显示名称。|  
|**replyto_address**|**nvarchar(128)**|对于来自此帐户的消息发送答复的地址。|  
|**servertype**|**sysname**|用于此帐户的电子邮件服务器的类型。|  
|**servername**|**sysname**|用于此帐户的电子邮件服务器的名称。|  
|**port**|**int**|电子邮件服务器使用的端口号。|  
|**username**|**nvarchar(128)**|登录电子邮件服务器所用的用户名（如果电子邮件服务器使用身份验证）。 当**用户名**为 NULL，数据库邮件不使用此帐户的身份验证。|  
|**use_default_credentials**|**bit**|指定是否使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]的凭据将邮件发送到 SMTP 服务器。 **use_default_credentials**位，无默认值。 当此参数为 1 时，数据库邮件使用 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]服务的凭据。 此参数为 0 时，数据库邮件使用 **@username** 和 **@password**  SMTP 服务器上进行身份验证。 如果 **@username** 和 **@password** 都为空，则数据库邮件将使用匿名身份验证。 在指定此参数之前，请咨询您的 SMTP 管理员。|  
|**enable_ssl**|**bit**|指定数据库邮件是否使用安全套接字层 (SSL) 对通信进行加密。 如果 SMTP 服务器需要 SSL，则使用该选项。 **enable_ssl**位，无默认值。 1 指示数据库邮件使用 SSL 对通信进行加密。 0 指示数据库邮件发送未使用 SSL 进行加密的邮件。|  
  
## <a name="remarks"></a>注释  
 如果没有*account_id*或*account_name*提供， **sysmail_help_account**列出了 Microsoft SQL Server 实例中的所有数据库邮件帐户的信息。  
  
 存储的过程**sysmail_help_account_sp**处于**msdb**数据库，而且由拥有**dbo**架构。 如果当前数据库不是，必须使用由三部分名称执行过程**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认为成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 **A.列出所有帐户的信息**  
  
 以下示例列出该实例所有帐户的帐户信息。  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp ;  
```  
  
 下面是示例结果集，由于行的长度原因而进行了编辑：  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- --------------------------------------- ------------------------- -------------------------------- --------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
149         Audit Account                Account for audit e-mail.               audit@Adventure-Works.com Automated Mailer (Audit)         NULL            SMTP       smtp.Adventure-Works.com  25          NULL 0                          0        
```  
  
 **B.列出特定帐户的信息**  
  
 以下示例列出名为 `AdventureWorks Administrator` 的帐户信息。  
  
```  
EXECUTE msdb.dbo.sysmail_help_account_sp  
    @account_name = 'AdventureWorks Administrator' ;  
```  
  
 下面是示例结果集，由于行的长度原因而进行了编辑：  
  
```  
account_id  name                         description                             email_address             display_name                     replyto_address servertype servername                port        username use_default_credentials enable_ssl  
----------- ---------------------------- ------------------------------------------------------ ------------------------- ---------------- ---------- ------------------------- ----------- -------- ----------------------- ----------  
148         AdventureWorks Administrator Mail account for administrative e-mail. dba@Adventure-Works.com   AdventureWorks Automated Mailer  NULL            SMTP       smtp.Adventure-Works.com  25          NULL     0                       0       
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
