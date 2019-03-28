---
title: sysmail_delete_profile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_delete_profile_sp
- sysmail_delete_profile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_profile_sp
ms.assetid: 71998653-4a02-446d-b6f7-50646a29e8a2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 601be3bb276576aaaf4c13e42e09d0de41b3b0f7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527979"
---
# <a name="sysmaildeleteprofilesp-transact-sql"></a>sysmail_delete_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除数据库邮件使用的邮件配置文件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_delete_profile_sp  { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>参数  
`[ @profile_id = ] profile_id` 是要删除的配置文件的配置文件 id。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @profile_name = ] 'profile_name'` 是要删除的配置文件的名称。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 删除配置文件不会删除配置文件使用的帐户。  
  
 此存储过程删除配置文件时，不考虑用户是否有权访问该配置文件。 删除用户的默认专用配置文件或默认公共配置文件时要格外小心**msdb**数据库。 没有默认配置文件不可用， **sp_send_dbmail**需要作为参数的配置文件的名称。 因此，删除默认的配置文件可能会导致调用**sp_send_dbmail**失败。 有关详细信息，请参阅[sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。  
  
 存储的过程**sysmail_delete_profile_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 以下示例将删除名为 `AdventureWorks Administrator` 的配置文件。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
