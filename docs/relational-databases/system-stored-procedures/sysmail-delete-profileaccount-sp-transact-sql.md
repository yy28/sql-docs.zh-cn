---
title: sysmail_delete_profileaccount_sp (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profileaccount_sp
- sysmail_delete_profileaccount_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profileaccount_sp
ms.assetid: b58d06f2-d6c9-4c8e-95bd-027c50f4621a
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0f80f3e20b32cb7571e1be5e77aa9eba1256dc74
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysmaildeleteprofileaccountsp-transact-sql"></a>sysmail_delete_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从数据库邮件配置文件中删除帐户。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_delete_profileaccount_sp  {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    {   [ @account_id = ] account_id | [ @account_name = ] 'account_name' }  
```  
  
## <a name="arguments"></a>参数  
 [ **@profile_id** =] *profile_id*  
 要删除的配置文件的配置文件 ID。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*可指定。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 要删除的配置文件的配置文件名。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*可指定。  
  
 [ **@account_id** = ] *account_id*  
 要删除的帐户 ID。 *account_id*是**int**，默认值为 NULL。 任一*account_id*或*account_name*可指定。  
  
 [ **@account_name** = ] **'***account_name***'**  
 要删除的帐户的名称。 *account_name*是**sysname**，默认值为 NULL。 任一*account_id*或*account_name*可指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 如果指定的帐户与指定的配置文件不相关，则会返回错误。  
  
 如果指定了帐户但没有指定配置文件，此存储过程会从所有配置文件中删除指定的帐户。 例如，如果您准备关闭现有的 SMTP 服务器，您将会从所有配置文件中删除使用该 SMTP 服务器的帐户，而不是从各个配置文件中删除每一个帐户。  
  
 如果指定了配置文件但没有指定帐户，此存储过程将从指定的配置文件中删除所有帐户。 例如，如果您正在更改配置文件使用的 SMTP 服务器，则可方便地从配置文件中删除所有帐户，然后根据需要添加新帐户。  
  
 存储的过程**sysmail_delete_profileaccount_sp**处于**msdb**数据库，而且由拥有**dbo**架构。 如果当前数据库不是，必须使用由三部分名称执行过程**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认为成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例显示了如何从配置文件 `Audit Account` 中删除帐户 `AdventureWorks Administrator`。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator',  
    @account_name = 'Audit Account' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
