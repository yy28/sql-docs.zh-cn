---
title: sp_add_operator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_operator
- sp_add_operator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_add_operator
ms.assetid: 817cd98a-4dff-4ed8-a546-f336c144d1e0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c1a6a9e45b1640a82cd15074373f162a97d9a0a6
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494071"
---
# <a name="spaddoperator-transact-sql"></a>sp_add_operator (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建用于警报和作业的操作员（通知收件人）。  
  
 
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_operator [ @name = ] 'name'   
     [ , [ @enabled = ] enabled ]   
     [ , [ @email_address = ] 'email_address' ]   
     [ , [ @pager_address = ] 'pager_address' ]   
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
`[ @name = ] 'name'` 操作员 （通知收件人） 的名称。 此名称必须唯一且不能含有百分比 (**%**) 字符。 *名称*是**sysname**，无默认值。  
  
`[ @enabled = ] enabled` 指示操作员的当前状态。 *已启用*是**tinyint**，默认值为**1** （启用）。 如果**0**，运算符未启用，并且不会收到通知。  
  
`[ @email_address = ] 'email_address'` 操作员电子邮件地址。 此字符串将直接传递到电子邮件系统。 *email_address*是**nvarchar(100)**，默认值为 NULL。  
  
 您可以指定物理电子邮件地址或别名*email_address*。 例如：  
  
 '**jdoe**或**jdoe@xyz.com**  
  
> [!NOTE]  
>  必须对数据库邮件使用电子邮件地址。  
  
`[ @pager_address = ] 'pager_address'` 操作员寻呼地址。 此字符串将直接传递到电子邮件系统。 *pager_address*是**narchar(100)**，默认值为 NULL。  
  
`[ @weekday_pager_start_time = ] weekday_pager_start_time` 此时间后，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]代理将寻呼通知发送给指定操作员在工作日，从星期一到星期五。 *weekday_pager_start_time*是**int**，默认值为**090000**，指示上午 9:00。 并且必须使用 HHMMSS 格式输入。  
  
`[ @weekday_pager_end_time = ] weekday_pager_end_time` 此时间后， **SQLServerAgent**服务不再发送寻呼通知向指定操作员在平日，从星期一到星期五。 *weekday_pager_end_time*是**int**，默认值为 180000，表示下午 6:00 并且必须使用 HHMMSS 格式输入。  
  
`[ @saturday_pager_start_time = ] saturday_pager_start_time` 此时间后， **SQLServerAgent**服务在星期六将寻呼通知发送到指定的运算符。 *saturday_pager_start_time*是**int**，默认值为 090000，表示上午 9:00。 并且必须使用 HHMMSS 格式输入。  
  
`[ @saturday_pager_end_time = ] saturday_pager_end_time` 此时间后， **SQLServerAgent**服务在星期六中不再将寻呼通知发送到指定的运算符。 *saturday_pager_end_time*是**int**，默认值为**180000**，这表示下午 6:00 并且必须使用 HHMMSS 格式输入。  
  
`[ @sunday_pager_start_time = ] sunday_pager_start_time` 此时间后， **SQLServerAgent**服务在星期日将寻呼通知发送到指定的运算符。 *sunday_pager_start_time*是**int**，默认值为**090000**，指示上午 9:00。 并且必须使用 HHMMSS 格式输入。  
  
`[ @sunday_pager_end_time = ] sunday_pager_end_time` 此时间后， **SQLServerAgent**服务在星期日中不再将寻呼通知发送到指定的运算符。 *sunday_pager_end_time*是**int**，默认值为**180000**，这表示下午 6:00 并且必须使用 HHMMSS 格式输入。  
  
`[ @pager_days = ] pager_days` 是一个数字，指示该运算符 （受限于指定的开始/结束时间） 的寻呼的天数。 *pager_days*是**tinyint**，默认值为**0** ，该值指示该运算符永远不会是可以接收到一个页面。 有效值为从**0**通过**127**。 *pager_days*通过将所需天数的对应值相加。 例如，从星期一到星期五是**2**+**4**+**8**+**16** + **32** = **62**。 下表列出了一周中每天的值。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|星期日|  
|**2**|星期一|  
|**4**|星期二|  
|**8**|星期三|  
|**16**|星期四|  
|**32**|星期五|  
|**64**|星期六|  
  
`[ @netsend_address = ] 'netsend_address'` 向其发送网络消息的操作员网络地址。 *netsend_address*是**nvarchar(100)**，默认值为 NULL。  
  
`[ @category_name = ] 'category'` 此运算符类别的名称。 *类别*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 **sp_add_operator**必须从运行**msdb**数据库。  
  
 电子邮件系统支持寻呼，如果想使用寻呼，则该系统必须有将电子邮件发送到寻呼程序的功能。  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 为管理作业提供了一种图形化的简便方法，建议使用此方法来创建和管理作业基础结构。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_add_operator**。  
  
## <a name="examples"></a>示例  
 下面的示例设置 `danwi` 的操作员信息。 操作员已被启用。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理通过寻呼在星期一到星期五的上午 8 点 至下午 5 点发送通知。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_operator  
    @name = N'Dan Wilson',  
    @enabled = 1,  
    @email_address = N'danwi',  
    @pager_address = N'5551290AW@pager.Adventure-Works.com',  
    @weekday_pager_start_time = 080000,  
    @weekday_pager_end_time = 170000,  
    @pager_days = 62 ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_help_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
