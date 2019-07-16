---
title: sysmail_help_status_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_status_sp
- sysmail_help_status_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_status_sp
ms.assetid: b44277c6-81e8-4b4d-85b3-a2f04d602e7a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 764b6154885dbd361f7d7d4a09d8e340b4a62ef5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044461"
---
# <a name="sysmailhelpstatussp-transact-sql"></a>sysmail_help_status_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  显示数据库邮件队列的状态。 使用**sysmail_start_sp**若要启动数据库邮件队列并**sysmail_stop_sp**停止数据库邮件队列。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_status_sp  
```  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**“状态”**|**nvarchar(7)**|数据库邮件的状态。 可能的值为**STARTED**并**已停止**。|  
  
## <a name="permissions"></a>权限  
 默认情况下，只有的成员**sysadmin**固定的服务器角色才能访问此过程。  
  
## <a name="examples"></a>示例  
 以下示例显示数据库邮件的状态。  
  
```  
EXECUTE msdb.dbo.sysmail_help_status_sp ;  
GO  
```  
  
 结果集：  
  
```  
Status  
-------  
STARTED  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件外部程序](../../relational-databases/database-mail/database-mail-external-program.md)   
 [sysmail_start_sp &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql.md)   
 [sysmail_stop_sp (Transact-SQL)](../../relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql.md)  
  
  
