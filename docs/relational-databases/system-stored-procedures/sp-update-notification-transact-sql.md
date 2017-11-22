---
title: "sp_update_notification (Transact SQL) |Microsoft 文档"
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
- sp_update_notification_TSQL
- sp_update_notification
dev_langs: TSQL
helpviewer_keywords: sp_updatenotification
ms.assetid: 3e1c3d40-8c24-46ce-a68e-ce6c6a237fda
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44b2755dca0a8d3cd2dae7d11e12cc16a708fe1e
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spupdatenotification-transact-sql"></a>sp_update_notification (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新警报通知的通知方法。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_notification  
          [@alert_name =] 'alert' ,  
     [@operator_name =] 'operator' ,  
     [@notification_method =] notification  
```  
  
## <a name="arguments"></a>参数  
 [  **@alert_name =**] *警报*  
 与该通知关联的警报的名称。 *警报*是**sysname**，无默认值。  
  
 [  **@operator_name =**] *运算符*  
 警报发生时要通知的操作员。 *运算符*是**sysname**，无默认值。  
  
 [  **@notification_method =**]*通知*  
 通知操作员的方法。 *通知*是**tinyint**，无默认值，并且可将一个或多个这些值。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|电子邮件|  
|**2**|寻呼程序|  
|**4**|**net send**|  
|**7**|所有方法|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_update_notification**必须从运行**msdb**数据库。  
  
 你可以更新通知操作员用户没有使用指定的必需的地址信息的*notification_method*。 如果发送电子邮件或寻呼通知时出现故障，则该故障将记录到 Microsoft SQL Server 代理程序错误日志中。  
  
## <a name="permissions"></a>Permissions  
 若要运行此存储的过程，必须授予用户**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
 下面的示例修改发送给通知的通知方法`François Ajenstat`警报`Test Alert`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_notification  
   @alert_name = N'Test Alert',  
   @operator_name = N'François Ajenstat',  
   @notification_method = 7;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_notification &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)   
 [sp_delete_notification &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-delete-notification-transact-sql.md)   
 [sp_help_notification &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-notification-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
