---
title: "sp_update_operator (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38da9010e434570fbcd75e026f11c50450e10691
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="spupdateoperator-transact-sql"></a>sp_update_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更新警报和作业所用的操作员（通知收件人）信息。  
  
   ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_operator   
     [ @name =] 'name'   
     [ , [ @new_name = ] 'new_name' ]   
     [ , [ @enabled = ] enabled]   
     [ , [ @email_address = ] 'email_address' ]  
     [ , [ @pager_address = ] 'pager_number']   
     [ , [ @weekday_pager_start_time = ] weekday_pager_start_time ]  
     [ , [ @weekday_pager_end_time = ] weekday_pager_end_time ]   
     [ , [ @saturday_pager_start_time = ] saturday_pager_start_time ]  
     [ , [ @saturday_pager_end_time = ] saturday_pager_end_time ]   
     [ , [ @sunday_pager_start_time = ] sunday_pager_start_time ]  
     [ , [ @sunday_pager_end_time = ] sunday_pager_end_time ]   
     [ , [ @pager_days = ] pager_days ]   
     [ , [ @netsend_address = ] 'netsend_address' ]   
     [ , [ @category_name = ] 'category' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @name=] '*name*'  
 要修改的操作员的名称。 *名称*是**sysname**，无默认值。  
  
 [ @new_name=] '*new_name*'  
 操作员的新名称。 此名称必须唯一。 *new_name*是**sysname**，默认值为 NULL。  
  
 [ @enabled=] *enabled*  
 一个数字，指示该运算符的当前状态 (**1**如果当前启用了， **0**如果没有)。 *启用*是**tinyint**，默认值为 NULL。 如果未启用，操作员将不接收警报通知。  
  
 [ @email_address=] '*email_address*'  
 操作员的电子邮件地址。 此字符串将直接传递到电子邮件系统。 *电子邮件地址*是**nvarchar(100)**，默认值为 NULL。  
  
 [ @pager_address=] '*pager_number*'  
 操作员的寻呼地址。 此字符串将直接传递到电子邮件系统。 *pager_number*是**nvarchar(100)**，默认值为 NULL。  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 指定从星期一到星期五可向此操作员发送寻呼通知的时间段的开始时间。 *weekday_pager_start_time*是**int**，默认值为 NULL，并且必须在使用的窗体 HHMMSS 中输入与 24 小时制。  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 指定从星期一到星期五可向此操作员发送寻呼通知的时间段的结束时间。 *weekday_pager_end_time*是**int**，默认值为 NULL，并且必须在使用的窗体 HHMMSS 中输入与 24 小时制。  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 指定在星期六可向指定操作员发送寻呼通知的时间段的开始时间。 *saturday_pager_start_time*是**int**，默认值为 NULL，并且必须在使用的窗体 HHMMSS 中输入与 24 小时制。  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 指定在星期六可向指定操作员发送寻呼通知的时间段的结束时间。 *saturday_pager_end_time*是**int**，默认值为 NULL，并且必须在使用的窗体 HHMMSS 中输入与 24 小时制。  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 指定在星期日可向指定操作员发送寻呼通知的时间段的开始时间。 *sunday_pager_start_time*是**int**，默认值为 NULL，并且必须在使用的窗体 HHMMSS 中输入与 24 小时制。  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 指定在星期日可向指定操作员发送寻呼通知的时间段的结束时间。 *sunday_pager_end_time*是**int**，默认值为 NULL，并且必须在使用的窗体 HHMMSS 中输入与 24 小时制。  
  
 [ @pager_days=] *pager_days*  
 指定操作员可以接收寻呼的天数（取决于指定的起始/结束时间）。 *pager_days*是**tinyint**，默认值为 NULL，并且必须是一个介于**0**通过**127**。 *pager_days*计算通过将各个值添加为所需的天数。 例如，从星期一到星期五是**2**+**4**+**8**+**16** + **32** = **64**。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**4**|星期二|  
|**8**|星期三|  
|**16**|星期四|  
|**32**|星期五|  
|**64**|星期六|  
  
 [ @netsend_address=] '*netsend_address*'  
 要将网络消息发送到的操作员的网络地址。 *netsend_address*是**nvarchar(100)**，默认值为 NULL。  
  
 [ @category_name=] '*category*'  
 该警报的类别名称。 *类别*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 sp_update_operator 必须基于 msdb 数据库运行。  
  
## <a name="permissions"></a>权限  
 默认情况下授予 sysadmin 固定服务器角色的成员执行此过程的权限。  
  
## <a name="examples"></a>示例  
 以下示例将操作员状态更新为启用，并设置可以寻呼 该操作员的时间（星期一至星期五，早上八点至下午五点）。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_operator   
    @name = N'François Ajenstat',  
    @enabled = 1,  
    @email_address = N'françoisa',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 64 ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
