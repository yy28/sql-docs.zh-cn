---
title: sysmail_update_principalprofile_sp (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysmail_update_principalprofile_sp
- sysmail_update_principalprofile_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_update_principalprofile_sp
ms.assetid: 9fe96e9a-4758-4e4a-baee-3e1217c4426c
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a86fc4775ee1096d72451ace855bb19a1094c3c5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
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
 [ **@principal_id** = ] *principal_id*  
 数据库用户或角色中的 ID **msdb**关联后，若要更改的数据库。 *principal_id*是**int**，默认值为 NULL。 任一*principal_id*或*principal_name*必须指定。  
  
 [ **@principal_name** = ] **'***principal_name***'**  
 数据库用户或角色中的名称**msdb**关联，以更新数据库。 *principal_name*是**sysname**，默认值为 NULL。 任一*principal_id*或*principal_name*可指定。  
  
 [ **@profile_id** =] *profile_id*  
 要更改的关联的配置文件的 ID。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 要更改的关联的配置文件的名称。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
 [ **@is_default** = ] **'***is_default***'**  
 指定此配置文件是否为数据库用户的默认配置文件。 数据库用户只能有一个默认的配置文件。 *is_default*是**位**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 InclusionThresholdSetting  
  
## <a name="remarks"></a>注释  
 此存储过程会更改指定的配置文件是否为数据库用户的默认配置文件。 一个数据库用户只能有一个默认专用配置文件。  
  
 关联的主体名称时**公共**或关联的主体 id 是**0**，则此存储的过程更改公共配置文件。 只能有一个默认的公共配置文件。  
  
 当**@is_default**是**1**并且主体是与多个配置文件关联，则指定的配置文件的主体将成为默认配置文件。 以前的默认配置文件仍与主体数据库关联，但不再是默认配置文件。  
  
 存储的过程**sysmail_update_principalprofile_sp**处于**msdb**数据库，而且由拥有**dbo**架构。 如果当前数据库不是，必须使用由三部分名称执行过程**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认为成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 **A.设置数据库的默认公共配置文件的配置文件**  
  
 下面的示例设置配置文件`General Use Profile`要默认公共配置文件中的用户**msdb**数据库。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'General Use Profile',  
    @is_default = '1';  
```  
  
 **B.设置配置文件将在用户的默认专用配置文件**  
  
 下面的示例设置配置文件`AdventureWorks Administrator`为主体数据库的默认配置文件`ApplicationUser`中**msdb**数据库。 该配置文件必须已与主体关联。 以前的默认配置文件仍与主体数据库关联，但不再是默认配置文件。  
  
```  
EXECUTE msdb.dbo.sysmail_update_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator',  
    @is_default = '1' ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
