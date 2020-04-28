---
title: sp_changesubscriber （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber
- sp_changesubscriber_TSQL
helpviewer_keywords:
- sp_changesubscriber
ms.assetid: d453c451-e957-490f-b968-5e03aeddaf10
author: stevestein
ms.author: sstein
ms.openlocfilehash: 42b56712e8b441184d55bf12ce16dbcb55930374
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68762781"
---
# <a name="sp_changesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  更改订阅服务器的选项。 更新针对此发布服务器的订阅服务器的任何分发任务。 此存储过程将写入到分发数据库中的**MSsubscriber_info**表。 此存储过程在发布服务器上对发布数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changesubscriber [ @subscriber= ] 'subscriber'  
    [ , [ @type= ] type ]  
    [ , [ @login= ] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @commit_batch_size= ] commit_batch_size ]  
    [ , [ @status_batch_size= ] status_batch_size ]  
    [ , [ @flush_frequency= ] flush_frequency ]  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @security_mode= ] security_mode ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @subscriber = ] 'subscriber'`要更改其选项的订阅服务器的名称。 *订阅服务器*的**sysname**，无默认值。  
  
`[ @type = ] type`订阅服务器类型。 *类型*为**tinyint**，默认值为 NULL。 **0**表示[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。 **1**指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或其他 ODBC 数据源服务器订阅服务器。  
  
`[ @login = ] 'login'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证登录 ID。 login 的数据类型为 sysname，默认值为 NULL******。  
  
`[ @password = ] 'password'`[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证密码。 *password*的值为**sysname**，默认值**%** 为。 **%** 指示密码属性未更改。  
  
`[ @commit_batch_size = ] commit_batch_size`仅支持向后兼容性。  
  
`[ @status_batch_size = ] status_batch_size`仅支持向后兼容性。  
  
`[ @flush_frequency = ] flush_frequency`仅支持向后兼容性。  
  
`[ @frequency_type = ] frequency_type`用于计划分发任务的频率。 *frequency_type*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|一次性|  
|**2**|按需|  
|**4**|每日|  
|**8**|每周|  
|**超过**|每月一次|  
|**32**|与“每月”选项相关|  
|**64**|自动启动|  
|**128**|重复执行|  
  
`[ @frequency_interval = ] frequency_interval`*Frequency_type*的间隔。 *frequency_interval*的值为**int**，默认值为 NULL。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval`分发任务的日期。 如果*frequency_type*设置为**32** （每月相对），则使用此参数。 *frequency_relative_interval*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|秒|  
|**4**|第三个|  
|**8**|第四个|  
|**超过**|最后一个|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor`分发任务在定义的*frequency_type*期间应定期发生的频率。 *frequency_recurrence_factor*的值为**int**，默认值为 NULL。  
  
`[ @frequency_subday = ] frequency_subday`在定义的时间段内重新计划的频率。 *frequency_subday*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|秒|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval`*Frequence_subday*的间隔。 *frequency_subday_interval*的值为**int**，默认值为 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day`第一次安排分发任务的时间，格式为 HHMMSS。 *active_start_time_of_day*的值为**int**，默认值为 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day`停止安排分发任务的时间，格式为 HHMMSS。 *active_end_time_of_day*的值为**int**，默认值为 NULL。  
  
`[ @active_start_date = ] active_start_date`第一次安排分发任务的日期，格式为 YYYYMMDD。 *active_start_date*的值为**int**，默认值为 NULL。  
  
`[ @active_end_date = ] active_end_date`停止安排分发任务的日期，格式为 YYYYMMDD。 *active_end_date*的值为**int**，默认值为 NULL。  
  
`[ @description = ] 'description'`可选的文本说明。 *description*的值为**nvarchar （255）**，默认值为 NULL。  
  
`[ @security_mode = ] security_mode`实现的安全模式。 *security_mode*为**int**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证|  
|**1**|Windows 身份验证|  
  
`[ @publisher = ] 'publisher'`指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*的**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *publisher*更改[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器上的项目属性时，不应使用 publisher。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changesubscriber**在所有类型的复制中使用。  
  
## <a name="permissions"></a>权限  
 只有**sysadmin**固定服务器角色的成员才能**sp_changesubscriber**执行。  
  
## <a name="see-also"></a>另请参阅  
 [sp_addsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
