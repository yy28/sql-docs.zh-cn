---
title: sysmail_update_profileaccount_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_profileaccount_sp_TSQL
- sysmail_update_profileaccount_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_profileaccount_sp
ms.assetid: 92ca7488-29db-414e-8e36-08b0a8f542bb
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 96dc0a33c15f1547088c3fe7c79824da55cd1d35
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58538119"
---
# <a name="sysmailupdateprofileaccountsp-transact-sql"></a>sysmail_update_profileaccount_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新数据库邮件配置文件中帐户的序列号。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_update_profileaccount_sp  { [ @profile_id = ] profile_id   
| [ @profile_name = ] 'profile_name' } ,  
    { [ @account_id = ] account_id | [ @account_name = ] 'account_name' } ,  
    [ @sequence_number = ] sequence_number  
```  
  
## <a name="arguments"></a>参数  
`[ @profile_id = ] profile_id` 要更新该配置文件的配置文件 ID。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @profile_name = ] 'profile_name'` 要更新的配置文件配置文件名称。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @account_id = ] account_id` 要更新的帐户 ID。 *account_id*是**int**，默认值为 NULL。 任一*account_id*或*account_name*必须指定。  
  
`[ @account_name = ] 'account_name'` 要更新的帐户的名称。 *account_name*是**sysname**，默认值为 NULL。 任一*account_id*或*account_name*必须指定。  
  
`[ @sequence_number = ] sequence_number` 新的帐户的序列号。 *sequence_number*是**int**，无默认值。 序列号可以确定帐户在配置文件中的使用顺序。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 如果指定的帐户与指定的配置文件不相关，则会返回错误。  
  
 序列号可以确定数据库邮件使用配置文件中帐户的顺序。 对于新的电子邮件，数据库邮件将从序列号最小的帐户开始。 如果该帐户失败，数据库邮件就使用具有下一个序列号较大的帐户，依此类推，直到数据库邮件成功发送邮件，或者序列号最大的帐户也失败为止。 如果具有最高序列号的帐户失败，则电子邮件发送失败。  
  
 如果存在具有相同序列号的多个帐户，则数据库邮件将仅使用其中一个帐户发送给定的电子邮件。 在此情况下，数据库邮件不能保证使用具有该序列号的特定帐户，也不能保证使用同一个帐户发送各个邮件。  
  
 存储的过程**sysmail_update_profileaccount_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例更改帐户的序列号`Admin-BackupServer`的配置文件内`AdventureWorks Administrator`中**msdb**数据库。 执行此代码后，该帐户的序列号为 `3`，指示前两个帐户失败后将尝试使用此帐户。  
  
```  
EXECUTE msdb.dbo.sysmail_update_profileaccount_sp  
    @profile_name = 'AdventureWorks Administrator'  
    ,@account_name = 'Admin-BackupServer',  
    ,@sequence_number = 3;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
