---
title: "sp_add_notification (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_add_notification_TSQL
- sp_add_notification
dev_langs: TSQL
helpviewer_keywords: sp_add_notification
ms.assetid: 0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c5bd95d4aee45046410211e77213fe4dcbc43fc3
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spaddnotification-transact-sql"></a>sp_add_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  设置警报通知。  
  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_notification [ @alert_name = ] 'alert' ,   
    [ @operator_name = ] 'operator' ,   
    [ @notification_method = ] notification_method  
```  
  
## <a name="arguments"></a>参数  
 [  **@alert_name=** ] *警报*  
 该通知的警报。 *警报*是**sysname**，无默认值。  
  
 [  **@operator_name=** ] *运算符*  
 当出现警报时通知操作员。 *运算符*是**sysname**，无默认值。  
  
 [  **@notification_method=** ] *notification_method*  
 通知操作员的方法。 *notification_method*是**tinyint**，无默认值。 *notification_method*可以是一个或多个与结合使用这些值**OR**逻辑运算符。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|电子邮件|  
|**2**|寻呼程序|  
|**4**|**net send**|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 无  
  
## <a name="remarks"></a>注释  
 **sp_add_notification**必须从运行**msdb**数据库。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 提供一种简单的图形方法来管理整个警报系统。 建议使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 配置警报基本结构。  
  
 若要发送响应警报的通知，必须首先配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理以发送邮件。  
  
 如果在发送电子邮件或寻呼通知时出现故障，则该故障将被记录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务错误日志中。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_add_notification**。  
  
## <a name="examples"></a>示例  
 以下示例为指定的警报 (`Test Alert`) 添加电子邮件通知。  
  
> **注意：**此示例假定`Test Alert`已存在且`François Ajenstat`是有效的运算符名称。  
  
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
 [sp_delete_notification &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [sp_update_notification &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-update-notification-transact-sql.md)   
 [sp_add_operator &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
