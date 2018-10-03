---
title: sysmail_add_profile_sp (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_add_profile_sp_TSQL
- sysmail_add_profile_sp
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_add_profile_sp
ms.assetid: a828e55c-633a-41cf-9769-a0698b446e6c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e62a0452a5e7e31591d368cbbcb2050272df5da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734725"
---
# <a name="sysmailaddprofilesp-transact-sql"></a>sysmail_add_profile_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建新的数据库邮件配置文件。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_add_profile_sp [ @profile_name = ] 'profile_name'  
    [ , [ @description = ] 'description' ]  
    [ , [ @profile_id = ] new_profile_id OUTPUT ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@profile_name** = ] **'***profile_name***'**  
 新配置文件的名称。 *profile_name*是**sysname**，无默认值。  
  
 [ **@description** = ] **'***description***'**  
 新配置文件的说明（可选）。 *描述*是**nvarchar(256)**，无默认值。  
  
 [ **@profile_id** = ] *new_profile_id***OUTPUT**  
 返回新配置文件的 ID。 *new_profile_id*是**int**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 数据库邮件配置文件可以保存任意数目的数据库邮件帐户。 数据库邮件存储过程可以通过配置文件名称或此过程生成的配置文件 ID 来引用配置文件。 有关将帐户添加到配置文件的详细信息，请参阅[sysmail_add_profileaccount_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-add-profileaccount-sp-transact-sql.md)。  
  
 可以使用存储过程更改的配置文件名称和描述**sysmail_update_profile_sp**，而该配置文件 id 保持不变的配置文件的整个生命周期。  
  
 配置文件名称对于 Microsoft [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 必须是唯一的，否则存储过程将返回一个错误。  
  
 存储的过程**sysmail_add_profile_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称执行该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 **A.创建新的配置文件**  
  
 以下示例将创建一个名为 `AdventureWorks Administrator` 的新数据库邮件配置文件。  
  
```  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.' ;  
```  
  
 **B.创建一个新的配置文件，将配置文件 id 保存在变量中**  
  
 以下示例将创建一个名为 `AdventureWorks Administrator` 的新数据库邮件配置文件。 该示例将配置文件 ID 号存储在变量 `@profileId` 中，并返回一个包含新配置文件的配置文件 ID 号的结果集。  
  
```  
DECLARE @profileId INT ;  
  
EXECUTE msdb.dbo.sysmail_add_profile_sp  
       @profile_name = 'AdventureWorks Administrator',  
       @description = 'Profile used for administrative mail.',  
       @profile_id = @profileId OUTPUT ;  
  
SELECT @profileId ;  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [创建数据库邮件帐户](../../relational-databases/database-mail/create-a-database-mail-account.md)   
 [数据库邮件配置对象](../../relational-databases/database-mail/database-mail-configuration-objects.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
