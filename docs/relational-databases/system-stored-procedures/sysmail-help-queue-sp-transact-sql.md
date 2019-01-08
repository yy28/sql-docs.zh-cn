---
title: sysmail_help_queue_sp (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_queue_sp
- sysmail_help_queue_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_queue_sp
ms.assetid: 94840482-112c-4654-b480-9b456c4c2bca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4ee5620aecfc4e263c16fb9c710b7a41e1564f6e
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590591"
---
# <a name="sysmailhelpqueuesp-transact-sql"></a>sysmail_help_queue_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  数据库邮件中具有两个队列：邮件队列和状态队列。 邮件队列存储正在等待发送的邮件项。 状态队列存储已发送项的状态。 此存储过程允许查看邮件队列的状态或状态队列的状态。 如果将参数**@queue_type**未指定，则存储的过程的每个队列返回一行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sysmail_help_queue_sp  [ @queue_type = ] 'queue_type'  
```  
  
## <a name="arguments"></a>参数  
 [ **@queue_type** =] **'**_queue_type_  
 可选参数，删除作为指定类型的电子邮件*queue_type*。 *queue_type*是**nvarchar(6)** ，无默认值。 有效输入包括**邮件**并**状态**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-set"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**queue_type**|**nvarchar(6)**|队列的类型。 可能的值为**邮件**并**状态**。|  
|**length**|**int**|指定队列中邮件项的数量。|  
|State|**nvarchar(64)**|监视器的状态。 可能的值为**非活动**（队列处于非活动状态）， **NOTIFIED** (队列已被通知发生)，并且**RECEIVES_OCCURRING** （接收队列）。|  
|**last_empty_rowset_time**|**日期时间**|上次队列为空的日期和时间。 采用军用时间格式和 GMT 时区。|  
|**last_activated_time**|**日期时间**|上次激活队列的日期和时间。 采用军用时间格式和 GMT 时区。|  
  
## <a name="remarks"></a>备注  
 当数据库邮件故障排除，使用**sysmail_help_queue_sp**若要查看队列中有多少项，状态队列，以及上一次激活。  
  
## <a name="permissions"></a>权限  
 默认情况下，只有的成员**sysadmin**固定的服务器角色才能访问此过程。  
  
## <a name="examples"></a>示例  
 以下示例返回邮件队列和状态队列。  
  
```  
EXECUTE msdb.dbo.sysmail_help_queue_sp ;  
GO  
```  
  
 此示例针对结果集的长度对结果集进行了编辑。  
  
```  
queue_type length      state              last_empty_rowset_time  last_activated_time  
---------- -------- ------------------ ----------------------- -----------------------  
mail       0        RECEIVES_OCCURRING 2005-10-07 21:14:47.010 2005-10-10 20:52:51.517  
status     0        INACTIVE           2005-10-07 21:04:47.003 2005-10-10 21:04:47.003  
  
(2 row(s) affected)  
  
```  
  
## <a name="see-also"></a>请参阅  
 [数据库邮件](../../relational-databases/database-mail/database-mail.md)  
  
  
