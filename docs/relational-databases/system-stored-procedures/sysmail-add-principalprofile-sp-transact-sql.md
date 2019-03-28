---
title: sysmail_add_principalprofile_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_principalprofile_sp_TSQL
- sysmail_add_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_principalprofile_sp
ms.assetid: b2a0b313-abb9-4c23-8511-db77ca8172b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf12b97028d3d98f7d5cc5ab034db95411d913dc
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58528499"
---
# <a name="sysmailaddprincipalprofilesp-transact-sql"></a>sysmail_add_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向数据库用户或角色授予使用数据库邮件配置文件的权限。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_add_principalprofile_sp  { [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ,  
    { [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' }  
    [ , [ @is_default ] = 'is_default' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @principal_id = ] principal_id` 数据库用户或角色中的 ID **msdb**的关联的数据库。 *principal_id*是**int**，默认值为 NULL。 任一*principal_id*或*principal_name*必须指定。 一个*principal_id*的**0**该配置文件将公共配置文件，在数据库中的所有主体授予访问权限。  
  
`[ @principal_name = ] 'principal_name'` 数据库用户或角色中的名称**msdb**的关联的数据库。 *principal_name*是**sysname**，默认值为 NULL。 任一*principal_id*或*principal_name*必须指定。 一个*principal_name*的 **'public'** 该配置文件将公共配置文件，在数据库中的所有主体授予访问权限。  
  
`[ @profile_id = ] profile_id` 关联的配置文件的 id。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @profile_name = ] 'profile_name'` 关联的配置文件的名称。 *profile_name*是**sysname**，无默认值。 任一*profile_id*或*profile_name*必须指定。  
  
`[ @is_default = ] is_default` 指定此配置文件是否为主体的默认配置文件。 主体必须且只能有一个默认配置文件。 *is_default*是**位**，无默认值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 若要使公共配置文件，指定**@principal_id**的**0**或**@principal_name**的**公共**。 公共配置文件可供中的所有用户**msdb**数据库，但用户还必须属于**DatabaseMailUserRole**执行**sp_send_dbmail**。  
  
 数据库用户只能有一个默认的配置文件。 当**@is_default**是**1**和用户已与一个或多个配置文件关联、 指定的配置文件将成为该用户的默认配置文件。 以前的默认配置文件仍与该用户关联，但不再是默认配置文件。  
  
 当**@is_default**是**0**并不存在其他关联，则存储的过程返回错误。  
  
 存储的过程**sysmail_add_principalprofile_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 **A.创建一个关联，设置默认配置文件**  
  
 下面的示例创建名为配置文件之间的关联`AdventureWorks Administrator Profile`并**msdb**数据库用户`ApplicationUser`。 此配置文件是该用户的默认配置文件。  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'ApplicationUser',  
    @profile_name = 'AdventureWorks Administrator Profile',  
    @is_default = 1 ;  
```  
  
 **B.将配置文件设置的默认公共配置文件**  
  
 以下示例使配置文件`AdventureWorks Public Profile`中的用户的默认公共配置文件**msdb**数据库。  
  
```  
EXECUTE msdb.dbo.sysmail_add_principalprofile_sp  
    @principal_name = 'public',  
    @profile_name = 'AdventureWorks Public Profile',  
    @is_default = 1 ;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
