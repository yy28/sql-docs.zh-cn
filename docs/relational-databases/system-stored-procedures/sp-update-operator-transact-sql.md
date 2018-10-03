---
title: sp_update_operator (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_operator_TSQL
- sp_update_operator
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_operator
ms.assetid: 231750a6-4828-4d03-afe6-b91d38c42ed3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ac1fb436ded0d829d9b6a9c8fe4e642f8de8cb16
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690315"
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
 [ @name=] '*名称*  
 要修改的操作员的名称。 *名称*是**sysname**，无默认值。  
  
 [ @new_name=] '*new_name*'  
 操作员的新名称。 此名称必须唯一。 *new_name*是**sysname**，默认值为 NULL。  
  
 [ @enabled=]*启用*  
 一个数字，指示操作员的当前状态 (**1**当前已启用，如果**0**如果没有)。 *已启用*是**tinyint**，默认值为 NULL。 如果未启用，操作员将不接收警报通知。  
  
 [ @email_address=] '*email_address*'  
 操作员的电子邮件地址。 此字符串将直接传递到电子邮件系统。 *email_address*是**nvarchar(100)**，默认值为 NULL。  
  
 [ @pager_address=] '*pager_number*'  
 操作员的寻呼地址。 此字符串将直接传递到电子邮件系统。 *pager_number*是**nvarchar(100)**，默认值为 NULL。  
  
 [ @weekday_pager_start_time=] *weekday_pager_start_time*  
 指定从星期一到星期五可向此操作员发送寻呼通知的时间段的开始时间。 *weekday_pager_start_time*是**int**，默认值为 NULL，且必须使用格式为 HHMMSS 输入 24 小时制。  
  
 [ @weekday_pager_end_time=] *weekday_pager_end_time*  
 指定从星期一到星期五可向此操作员发送寻呼通知的时间段的结束时间。 *weekday_pager_end_time*是**int**，默认值为 NULL，且必须使用格式为 HHMMSS 输入 24 小时制。  
  
 [ @saturday_pager_start_time=] *saturday_pager_start_time*  
 指定在星期六可向指定操作员发送寻呼通知的时间段的开始时间。 *saturday_pager_start_time*是**int**，默认值为 NULL，且必须使用格式为 HHMMSS 输入 24 小时制。  
  
 [ @saturday_pager_end_time=] *saturday_pager_end_time*  
 指定在星期六可向指定操作员发送寻呼通知的时间段的结束时间。 *saturday_pager_end_time*是**int**，默认值为 NULL，且必须使用格式为 HHMMSS 输入 24 小时制。  
  
 [ @sunday_pager_start_time=] *sunday_pager_start_time*  
 指定在星期日可向指定操作员发送寻呼通知的时间段的开始时间。 *sunday_pager_start_time*是**int**，默认值为 NULL，且必须使用格式为 HHMMSS 输入 24 小时制。  
  
 [ @sunday_pager_end_time=] *sunday_pager_end_time*  
 指定在星期日可向指定操作员发送寻呼通知的时间段的结束时间。 *sunday_pager_end_time*是**int**，默认值为 NULL，且必须使用格式为 HHMMSS 输入 24 小时制。  
  
 [ @pager_days=] *pager_days*  
 指定操作员可以接收寻呼的天数（取决于指定的起始/结束时间）。 *pager_days*是**tinyint**，默认值为 NULL，并且必须是一个介于**0**通过**127**。 *pager_days*通过将所需天数的对应值相加。 例如，从星期一到星期五是**2**+**4**+**8**+**16** + **32** = **64**。  
  
|ReplTest1|Description|  
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
  
 [ @category_name=] '*类别*  
 该警报的类别名称。 *类别*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 sp_update_operator 必须基于 msdb 数据库运行。  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>请参阅  
 [sp_add_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
