---
title: sysmail_help_configure_sp （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3d07f77c468bb14b28cd003f599bebd636d6f862
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056161"
---
# <a name="sysmail_help_configure_sp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示数据库邮件的配置设置。  
  
 ![“主题链接”图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @parameter_name = ] 'parameter_name'` 要检索的配置设置的名称。 指定时，将在 **\@parameter_value** OUTPUT 参数中返回配置设置的值。 如果未指定 **\@parameter_name** ，此存储过程将返回一个结果集，其中包含实例中的所有数据库邮件配置设置。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 如果未指定 **\@parameter_name** ，则返回包含以下列的结果集。  
  
||||  
|-|-|-|  
|列名|数据类型|描述|  
|**paramname**|**nvarchar(256)**|配置参数的名称。|  
|**paramvalue**|**nvarchar(256)**|配置参数的值。|  
|**description**|**nvarchar(256)**|配置参数的说明。|  
  
## <a name="remarks"></a>Remarks  
 存储过程**sysmail_help_configure_sp**列出实例的当前数据库邮件配置设置。  
  
 当指定 **\@parameter_name** ，但没有为 **\@parameter_value**提供输出参数时，此存储过程不会生成任何输出。  
  
 存储过程**sysmail_help_configure_sp**在**msdb**数据库中，由**dbo**架构拥有。 如果当前数据库不是**msdb**，则必须使用由三部分组成的名称来调用该过程。  
  
## <a name="permissions"></a>Permissions  
 此过程的执行权限默认授予**sysadmin**固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
 以下示例显示如何列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的数据库邮件配置设置。  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 下面是示例结果集，由于行的长度原因而进行了编辑：  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件存储过程&#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
