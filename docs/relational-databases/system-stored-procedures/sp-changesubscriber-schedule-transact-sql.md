---
title: sp_changesubscriber_schedule (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_changesubscriber_schedule
- sp_changesubscriber_schedule_TSQL
helpviewer_keywords:
- sp_changesubscriber_schedule
ms.assetid: ff84e8e2-d496-482c-b23e-38a6626596e6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: eb100fa06326ed377696d7e8677902bdb44c06b2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47688994"
---
# <a name="spchangesubscriberschedule-transact-sql"></a>sp_changesubscriber_schedule (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改订阅服务器的分发代理或合并代理调度。 此存储过程在发布服务器的任何数据库中执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_changesubscriber_schedule [ @subscriber = ] 'subscriber', [ @agent_type = ] type  
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
 [  **@subscriber=**] **'***订阅服务器*****  
 订阅服务器的名称。 *订阅服务器上*是**sysname**。 订阅服务器的名称必须在数据库中唯一，不能已经存在，不能为 NULL。  
  
 [  **@agent_type=**]*类型*  
 代理的类型。 *类型*是**smallint**，默认值为**0**。 **0**指示分发代理。 **1**指示合并代理。  
  
 [  **@frequency_type=**] *frequency_type*  
 安排分发任务所使用的频率。 *frequency_type*是**int**，默认值为**64**。 有 10 个计划列。  
  
 [  **@frequency_interval=**] *frequency_interval*  
 是应用于设置频率的值*frequency_type*。 *frequency_interval*是**int**，默认值为**1**。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 分发任务的日期。 *frequency_relative_interval*是**int**，默认值为**1**。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为**0**。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 在定义周期内重新调度的频率（分钟）。 *frequency_subday*是**int**，默认值为**4**。  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，默认值为**5**。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排分发任务的时间。 *active_start_time_of_day*是**int**，默认值为**0**。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排分发任务的时间。 *active_end_time_of_day*是**int**，默认值为**235959**，这意味着 11:59:59 PM 24 小时制。  
  
 [  **@active_start_date=**] *active_start_date*  
 第一次安排分发任务的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为**0**。  
  
 [  **@active_end_date=**] *active_end_date*  
 停止安排分发任务的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为**99991231**，表示 9999 年 12 月 31。  
  
 [ **@publisher**=] **'***发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*在更改项目属性时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changesubscriber_schedule**用于所有类型的复制。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_changesubscriber_schedule**。  
  
## <a name="see-also"></a>请参阅  
 [sp_addsubscriber_schedule &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-schedule-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
