---
description: sp_add_notification (Transact-SQL)
title: sp_add_notification (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_notification_TSQL
- sp_add_notification
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 0c009cd32cf3fdd92fbb638a00d5f1f4a024a1b8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493524"
---
# <a name="sp_add_notification-transact-sql"></a>sp_add_notification (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  设置警报通知。  
  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>参数  
`[ @alert_name = ] 'alert'` 此通知的警报。 *警报* 为 **sysname**，无默认值。  
  
`[ @operator_name = ] 'operator'` 警报发生时要通知的操作员。 *运算符* 的值为 **sysname**，无默认值。  
  
`[ @notification_method = ] notification_method` 通知操作员使用的方法。 *notification_method* 为 **tinyint**，无默认值。 *notification_method* 可以是与 **or** 逻辑运算符组合在一起的一个或多个值。  
  
|Value|说明|  
|-----------|-----------------|  
|**1**|电子邮件|  
|**2**|寻呼机|  
|**4**|**net send**|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>备注  
 必须从**msdb**数据库运行**sp_add_notification** 。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供一种简单的图形方法来管理整个警报系统。 建议使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 配置警报基本结构。  
  
 若要发送响应警报的通知，必须首先配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理以发送邮件。  
  
 如果在发送电子邮件或寻呼通知时出现故障，则该故障将被记录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务错误日志中。  
  
## <a name="permissions"></a>权限  
 只有 **sysadmin** 固定服务器角色的成员才能 **sp_add_notification**执行。  
  
## <a name="examples"></a>示例  
 以下示例为指定的警报 (`Test Alert`) 添加电子邮件通知。  
  
> **注意：** 此示例假定 `Test Alert` 已存在并且 `François Ajenstat` 是有效的运算符名称。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_notification  
 @alert_name = N'Test Alert',  
 @operator_name = N'François Ajenstat',  
 @notification_method = 1 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_delete_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [sp_add_operator &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
