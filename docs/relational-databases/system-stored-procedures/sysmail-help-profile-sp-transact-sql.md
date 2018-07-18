---
title: sysmail_help_profile_sp (Transact SQL) |Microsoft 文档
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
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4aa2e8bb227da4fdb3305c96de0be04cd4a877ea
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258208"
---
# <a name="sysmailhelpprofilesp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出有关一个或多个邮件配置文件的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@profile_id** =] *profile_id*  
 要返回其信息的配置文件 ID。 *profile_id*是**int**，默认值为 NULL。  
  
 [ **@profile_name** = ] **'***profile_name***'**  
 要返回其信息的配置文件名称。 *profile_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 返回包含以下列的结果集。  
  
||||  
|-|-|-|  
|列名|数据类型|Description|  
|**profile_id**|**int**|配置文件 ID。|  
|**名称**|**sysname**|配置文件名。|  
|**说明**|**nvarchar(256)**|配置文件的说明。|  
  
## <a name="remarks"></a>注释  
 当指定配置文件名称或配置文件 id，则**sysmail_help_profile_sp**返回有关该配置文件的信息。 否则为**sysmail_help_profile_sp**返回有关在每个配置文件信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
 存储的过程**sysmail_help_profile_sp**处于**msdb**数据库，而且由拥有**dbo**架构。 如果当前数据库不是，必须使用由三部分名称执行过程**msdb**。  
  
## <a name="permissions"></a>权限  
 执行此过程默认为成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 **A.列出所有配置文件**  
  
 以下示例显示如何列出实例中的所有配置文件。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp;  
```  
  
 下面是行长度经过调整的结果集示例：  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
57          AdventureWorks Operator       Operator mail profile.          
```  
  
 **B.列出特定的配置文件**  
  
 以下示例显示如何列出配置文件 `AdventureWorks Administrator` 的信息。  
  
```  
EXECUTE msdb.dbo.sysmail_help_profile_sp  
    @profile_name = 'AdventureWorks Administrator' ;  
```  
  
 下面是行长度经过调整的结果集示例：  
  
```  
profile_id  name                          description  
----------- ----------------------------- ------------------------------  
56          AdventureWorks Administrator  Administrative mail profile.    
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
