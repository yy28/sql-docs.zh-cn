---
title: sp_help_notification （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_notification
- sp_help_notification_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_notification
ms.assetid: 0273457f-9d2a-4a6f-9a16-6a6bf281cba0
author: stevestein
ms.author: sstein
ms.openlocfilehash: 630c2f90085cedfbb5c59ba395c7d0d9ae9d9643
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67906099"
---
# <a name="sp_help_notification-transact-sql"></a>sp_help_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告给定操作员的警报列表，或者报告给定警报的操作员列表。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_help_notification  
     [ @object_type = ] 'object_type' ,  
     [ @name = ] 'name' ,  
     [ @enum_type = ] 'enum_type' ,   
     [ @notification_method = ] notification_method   
     [ , [ @target_name = ] 'target_name' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @object_type = ] 'object_type'`要返回的信息的类型。 *object_type*为**char （9）**，无默认值。 *object_type*可以是警报，其中列出了分配给所提供的操作员名称的警报 *，或操作员，其中*列出了负责提供的警报名称的操作员 *。*  
  
`[ @name = ] 'name'`操作员名称（如果*object_type*为 OPERATORS）或警报名称（如果*object_type*为警报）。 *名称*为**sysname**，无默认值。  
  
`[ @enum_type = ] 'enum_type'`返回的*object_type*信息。 大多数情况下， *enum_type*是实际的。 *enum_type*为**char （10）**，无默认值，可以是下列值之一。  
  
|Value|说明|  
|-----------|-----------------|  
|ACTUAL|仅列出与*名称*关联的*object_types* 。|  
|ALL|列出所有*object_types*包括不与*name*关联的。|  
|TARGET|仅列出与所提供*target_name*匹配的*object_types* ，而不考虑与 name 关联的*名称*。|  
  
`[ @notification_method = ] notification_method`确定要返回的通知方法列的数值。 *notification_method*为**tinyint**，可以是下列值之一。  
  
|Value|说明|  
|-----------|-----------------|  
|**1**|电子邮件：只返回**use_email**列。|  
|**2**|寻呼：仅返回**use_pager**列。|  
|**4**|NetSend：仅返回**use_netsend**列。|  
|**7**|全部：返回全部列。|  
  
`[ @target_name = ] 'target_name'`要搜索的警报名称（如果*object_type*为警报）或要搜索的操作员名称（如果*object_type*为运算符）。 仅当*enum_type*为 target 时，才需要*target_name* 。 *target_name*的默认值为**sysname**，默认值为 NULL。  
  
## <a name="return-code-valves"></a>返回代码阀  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 如果*object_type*为**警报**，则结果集将列出给定操作员的所有警报。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**alert_id**|**int**|警报标识号。|  
|**alert_name**|**sysname**|警报名称。|  
|**use_email**|**int**|使用电子邮件通知操作员：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_pager**|**int**|使用寻呼通知操作员：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_netsend**|**int**|使用网络弹出消息通知操作员：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_email**|**int**|为此警报发送的电子邮件通知的次数。|  
|**has_pager**|**int**|为此警报发送的寻呼通知的次数。|  
|**has_netsend**|**int**|为此警报发送的**net send**通知数。|  
  
 如果**object_type**是**运算符**，则结果集将列出给定警报的所有运算符。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**operator_id**|**int**|操作员标识号。|  
|**operator_name**|**sysname**|操作员名称。|  
|**use_email**|**int**|使用电子邮件发送操作员的通知：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_pager**|**int**|使用寻呼发送操作员的通知：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**use_netsend**|**int**|用于通知操作员的网络弹出窗口：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_email**|**int**|操作员有电子邮件地址：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_pager**|**int**|操作员有寻呼地址：<br /><br /> **1** = 是<br /><br /> **0** = 否|  
|**has_netsend**|**int**|操作员已配置网络发送通知。<br /><br /> **1** = 是<br /><br /> **0** = 否|  
  
## <a name="remarks"></a>备注  
 必须从**msdb**数据库运行此存储过程。  
  
## <a name="permissions"></a>权限  
 若要执行此存储过程，用户必须为 **sysadmin** 固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-alerts-for-a-specific-operator"></a>A. 列出特定操作员的警报  
 以下示例返回操作员 `François Ajenstat` 接收与其相关的任何一种通知的所有警报。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_notification   
    @object_type = N'ALERTS',  
    @name = N'François Ajenstat',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
### <a name="b-listing-operators-for-a-specific-alert"></a>B. 列出特定警报的操作员  
 以下示例返回接收到 `Test Alert` 警报的任何一种通知的所有操作员。  
  
```  
USE msdb ;  
GO  
  
EXEC sp_help_notification  
    @object_type = N'OPERATORS',  
    @name = N'Test Alert',  
    @enum_type = N'ACTUAL',  
    @notification_method = 7 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
