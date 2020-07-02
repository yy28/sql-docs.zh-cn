---
title: sysmail_help_profile_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_profile_sp_TSQL
- sysmail_help_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_profile_sp
ms.assetid: d7169a8e-92b1-49eb-9124-3b2f69755ddb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5d98f997c2ab70060aa8770d73c8a8a4823c09bb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85752712"
---
# <a name="sysmail_help_profile_sp-transact-sql"></a>sysmail_help_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  列出有关一个或多个邮件配置文件的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_profile_sp  [   [ @profile_id = ] profile_id | [ @profile_name = ] 'profile_name' ]  
```  
  
## <a name="arguments"></a>自变量  
`[ @profile_id = ] profile_id`要为其返回信息的配置文件 id。 *profile_id*的值为**int**，默认值为 NULL。  
  
`[ @profile_name = ] 'profile_name'`要为其返回信息的配置文件名称。 *profile_name*的默认值为**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 返回包含以下列的结果集。  
  
||||  
|-|-|-|  
|列名称|数据类型|说明|  
|**profile_id**|**int**|配置文件 ID。|  
|name|**sysname**|配置文件名。|  
|**2008**|**nvarchar(256)**|配置文件的说明。|  
  
## <a name="remarks"></a>备注  
 指定配置文件名称或配置文件 id 时， **sysmail_help_profile_sp**返回有关该配置文件的信息。 否则， **sysmail_help_profile_sp**返回有关实例中的每个配置文件的信息 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。  
  
 存储过程**sysmail_help_profile_sp**在**msdb**数据库中，由**dbo**架构拥有。 如果当前数据库不是**msdb**，则必须使用由三部分组成的名称来执行该过程。  
  
## <a name="permissions"></a>权限  
 此过程的执行权限默认授予**sysadmin**固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
 **A. 列出所有配置文件**  
  
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
  
 **B. 列出特定配置文件**  
  
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
 [数据库邮件存储过程 &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
