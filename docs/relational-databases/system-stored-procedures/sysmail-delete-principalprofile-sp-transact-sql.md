---
title: sysmail_delete_principalprofile_sp (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- sysmail_delete_principalprofile_sp_TSQL
- sysmail_delete_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_delete_principalprofile_sp
ms.assetid: 8fc14700-e17a-4073-9a96-7fc23e775c69
caps.latest.revision: 43
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccfc4bfd03b7a7fba693bfd9e6eb86494057a665
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysmaildeleteprincipalprofilesp-transact-sql"></a>sysmail_delete_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除数据库用户或角色使用公共或专用数据库邮件配置文件的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_delete_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
```  
  
## <a name="arguments"></a>参数  
 [ **@principal_id** = ] *principal_id*  
 是数据库用户或角色中的 ID **msdb**关联后，若要删除的数据库。 *principal_id*是**int**，默认值为 NULL。 若要使公共配置文件成为专用配置文件，提供的主体 ID **0**或主体名称 **'public'**。 任一*principal_id*或*principal_name*必须指定。  
  
 [ **@principal_name** = ] **'***principal_name***'**  
 是数据库用户或角色中的名称**msdb**关联后，若要删除的数据库。 *principal_name*是**sysname**，默认值为 NULL。 若要使公共配置文件成为专用配置文件，提供的主体 ID **0**或主体名称 **'public'**。 任一*principal_id*或*principal_name*必须指定。  
  
 [ **@profile_id** =] *profile_id*  
 要删除的关联的配置文件的 ID。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 要删除的关联的配置文件的名称。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 若要使公共配置文件成为专用配置文件，提供 **'public'** 主体的名称或**0**主体 id。  
  
 删除用户的默认专用配置文件的权限或默认公共配置文件的权限时，请谨慎操作。 没有默认配置文件时可用， **sp_send_dbmail**需要作为自变量的配置文件的名称。 因此，删除默认的配置文件可能会导致调用**sp_send_dbmail**失败。 有关详细信息，请参阅[sp_send_dbmail &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql.md)。  
  
 存储的过程**sysmail_delete_principalprofile_sp**处于**msdb**数据库，而且由拥有**dbo**架构。 如果当前数据库不是，必须使用由三部分名称执行过程**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认为成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例演示删除的配置文件之间的关联**AdventureWorks 管理员**和登录名**ApplicationUser**中**msdb**数据库。  
  
```  
EXECUTE msdb.dbo.sysmail_delete_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
