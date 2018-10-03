---
title: sysmail_help_configure_sp (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 1ef80206f9ff82cf1ab2917e90f61432be15c190
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838425"
---
# <a name="sysmailhelpconfiguresp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示数据库邮件的配置设置。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [**@parameter_name** = ] **'***parameter_name***'**  
 要检索的配置设置名称。 如果指定，在返回的配置设置的值**@parameter_value**输出参数。 如果未**@parameter_name**指定，则此存储的过程返回的结果集包含所有实例中的数据库邮件配置设置。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 如果未**@parameter_name**指定时，返回的结果集包含以下列。  
  
||||  
|-|-|-|  
|列名|数据类型|Description|  
|**paramname**|**nvarchar(256)**|配置参数的名称。|  
|**paramvalue**|**nvarchar(256)**|配置参数的值。|  
|**description**|**nvarchar(256)**|配置参数的说明。|  
  
## <a name="remarks"></a>备注  
 存储的过程**sysmail_help_configure_sp**列出该实例的当前数据库邮件配置设置。  
  
 当**@parameter_name**指定，则为没有提供任何输出参数，但**@parameter_value**，此存储的过程会生成任何输出。  
  
 存储的过程**sysmail_help_configure_sp**处于**msdb**数据库中，归**dbo**架构。 必须使用由三部分名称调用该过程，如果当前数据库不是**msdb**。  
  
## <a name="permissions"></a>Permissions  
 执行此过程默认情况下的成员的权限**sysadmin**固定的服务器角色。  
  
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
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)   
 [数据库邮件存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
