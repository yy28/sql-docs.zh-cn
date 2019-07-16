---
title: sysmail_update_principalprofile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: dd9644253302c6a577c6cc3923bb3a9e3a0d8c0e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037378"
---
# <a name="sysmailupdateprincipalprofilesp-transact-sql"></a>sysmail_update_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新主体和配置文件之间的关联的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_update_principalprofile_sp { @principal_id = principal_id | @principal_name = 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ,  
    [ @is_default = ] 'is_default'  
```  
  
## <a name="arguments"></a>参数  
`[ @principal_id = ] principal_id` 数据库用户或角色中的 ID **msdb**要更改的关联的数据库。 *principal_id*是**int**，默认值为 NULL。 任一*principal_id*或*principal_name*必须指定。  
  
`[ @principal_name = ] 'principal_name'` 数据库用户或角色中的名称**msdb**要更新的关联的数据库。 *principal_name*是**sysname**，默认值为 NULL。 任一*principal_id*或*principal_name*可能指定。  
  
`[ @profile_id = ] profile_id` 要更改的关联的配置文件的 id。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @profile_name = ] 'profile_name'` 要更改的关联的配置文件的名称。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @is_default = ] 'is_default'` 是此配置文件是否是数据库用户的默认配置文件。 数据库用户只能有一个默认的配置文件。 *is_default*是**位**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 此存储过程会更改指定的配置文件是否为数据库用户的默认配置文件。 一个数据库用户只能有一个默认专用配置文件。  
  
 当关联的主体名称是**公共**或关联的主体 id 都**0**，则此存储的过程将更改公共配置文件。 只能有一个默认的公共配置文件。  
  
 当 **\@is_default**是**1**和主体与多个配置文件相关联，指定的配置文件的主体将成为默认配置文件。 以前的默认配置文件仍与主体数据库关联，但不再是默认配置文件。  
  
 存储的过程**sysmail_update_principalprofile_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 **A.一个配置文件数据库的默认公共配置文件设置**  
  
 下面的示例设置的配置文件`General Use Profile`中的用户的默认公共配置文件**msdb**数据库。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B.将用户的默认专用配置文件配置文件设置**  
  
 下面的示例设置的配置文件`AdventureWorks Administrator`主体的默认配置文件`ApplicationUser`中**msdb**数据库。 该配置文件必须已与主体关联。 以前的默认配置文件仍与主体数据库关联，但不再是默认配置文件。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
