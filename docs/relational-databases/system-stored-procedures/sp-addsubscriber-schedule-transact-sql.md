---
title: sp_addsubscriber_schedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber_schedule_TSQL
- sp_addsubscriber_schedule
helpviewer_keywords:
- sp_addsubscriber_schedule
ms.assetid: a6225033-5c3b-452f-ae52-79890a3590ed
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 18bd39f4c364f6bfa7383040722564e7cab65dbe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779375"
---
# <a name="spaddsubscriberschedule-transact-sql"></a>sp_addsubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为分发代理和合并代理添加计划。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addsubscriber_schedule [ @subscriber = ] 'subscriber'  
    [ , [ @agent_type = ] agent_type ]  
    [ , [ @frequency_type = ] frequency_type ]  
    [ , [ @frequency_interval = ] frequency_interval ]  
    [ , [ @frequency_relative_interval = ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor = ] frequency_recurrence_factor ]  
    [ , [ @frequency_subday = ] frequency_subday ]  
    [ , [ @frequency_subday_interval = ] frequency_subday_interval ]  
    [ , [ @active_start_time_of_day = ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day = ] active_end_time_of_day ]  
    [ , [ @active_start_date = ] active_start_date ]  
    [ , [ @active_end_date = ] active_end_date ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@subscriber =** ] **'***订阅服务器*****  
 订阅服务器的名称。 *订阅服务器上*是**sysname**。 订阅服务器的名称必须在数据库中唯一，不能已经存在，不能为 NULL。  
  
 [  **@agent_type =** ] *agent_type*  
 代理的类型。 *agent_type*是**smallint**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**0** （默认值）|分发代理|  
|**1**|合并代理|  
  
 [  **@frequency_type =** ] *frequency_type*  
 安排分发代理计划的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|按需|  
|**4**|每天|  
|**8**|每周|  
|**16**|每月|  
|**32**|与“每月”选项相关|  
|**64** （默认值）|自动启动|  
|**128**|重复执行|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 是要将应用于设置频率的值*frequency_type*。 *frequency_interval*是**int**，默认值为**1**。  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 分发代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1** （默认值）|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为**0**。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 在指定期内重新安排计划的频率。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4** （默认值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，默认值为**5**。  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 第一次安排分发代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为**0**。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 停止安排分发代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 235959，表示 11:59:59 PM 24 小时制。  
  
 [ **@active_start_date =** ] *active_start_date*  
 第一次安排分发代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为**0**。  
  
 [ **@active_end_date =** ] *active_end_date*  
 停止安排分发代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 99991231，表示年 12 月 31 日到 9999。  
  
 [  **@publisher =** ] **'***发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*不能为指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addsubscriber_schedule**快照复制、 事务复制和合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_addsubscriber_schedule**。  
  
## <a name="see-also"></a>请参阅  
 [sp_changesubscriber_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-schedule-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
