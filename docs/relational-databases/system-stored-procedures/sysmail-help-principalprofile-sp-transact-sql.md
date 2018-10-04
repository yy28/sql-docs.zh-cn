---
title: sysmail_help_principalprofile_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_principalprofile_sp_TSQL
- sysmail_help_principalprofile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_principalprofile_sp
ms.assetid: 0cfd6464-09c7-4f03-9d25-58001c096a9e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 04746f7694e4f3bef2a946398f0bc9d1e1808a3a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47739325"
---
# <a name="sysmailhelpprincipalprofilesp-transact-sql"></a>sysmail_help_principalprofile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出有关数据库邮件配置文件和数据库主体之间的关联的信息。  
  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_principalprofile_sp [ {   [ @principal_id = ] principal_id | [ @principal_name = ] 'principal_name' } ]  
    [ [ , ] {   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' } ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@principal_id=** ] *principal_id*  
 是数据库用户或角色中的 ID **msdb**关联要列出的数据库。 *principal_id*是**int**，默认值为 NULL。 任一*principal_id*或*principal_name*可能指定。  
  
 [ **@principal_name=** ] **'***principal_name***'**  
 是数据库用户或角色中的名称**msdb**关联要列出的数据库。 *principal_name*是**sysname**，默认值为 NULL。 任一*principal_id*或*principal_name*可能指定。  
  
 [  **@profile_id=** ] *profile_id*  
 关联要列出的配置文件的 ID。 *profile_id*是**int**，默认值为 NULL。 任一*profile_id*或*profile_name*可能指定。  
  
 [  **@profile_name=** ] **'***profile_name*****  
 关联要列出的配置文件的名称。 *profile_name*是**sysname**，默认值为 NULL。 任一*profile_id*或*profile_name*可能指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 返回一个结果集，其中包含下表中列出的列。  
  
||||  
|-|-|-|  
|列名|数据类型|Description|  
|**principal_id**|**int**|数据库用户的 ID。|  
|**principal_name**|**sysname**|数据库用户的名称。|  
|**profile_id**|**int**|数据库邮件配置文件的 ID 号。|  
|**profile_name**|**sysname**|数据库邮件配置文件的名称。|  
|**is_default**|**bit**|声明配置文件是否为用户的默认配置文件的标志。|  
  
## <a name="remarks"></a>备注  
 如果**sysmail_help_principalprofile_sp**调用不带参数，返回的结果集列出了所有的实例中的关联[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 否则，结果集将包含与所提供参数相匹配的关联的信息。 例如，提供配置文件名称时，该过程会列出配置文件的所有关联。  
  
 **sysmail_help_principalprofile_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 要求具有 **sysadmin** 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-information-for-a-specific-association"></a>A. 列出特定关联的信息  
 以下示例显示如何列出 `AdventureWorks Administrator` 数据库中 `ApplicationLogin` 配置文件和 `msdb` 主体之间的所有关联的信息。  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp  
    @principal_name = 'danw',  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 下面是行长度经过调整的示例结果集。  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
5            danw               9           AdventureWorks Administrator   1  
```  
  
### <a name="b-listing-information-for-all-associations"></a>B. 列出所有关联的信息  
 以下示例显示如何列出该实例中所有关联的信息。  
  
```  
EXECUTE msdb.dbo.sysmail_help_principalprofile_sp ;  
```  
  
 下面是行长度经过调整的示例结果集。  
  
```  
principal_id principal_name     profile_id  profile_name                   is_default  
------------ ------------------ ----------- ------------------------------ ----------  
6            terrid             3           Product Update Profile         1  
5            danw               9           AdventureWorks Administrator   1  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
