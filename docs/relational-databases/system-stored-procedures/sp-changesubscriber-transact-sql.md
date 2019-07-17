---
title: sp_changesubscriber (TRANSACT-SQL) |Microsoft Docs
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
ms.openlocfilehash: d18282229ec2f481aaab91aff8273bd9b3e72a34
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090061"
---
# <a name="spchangesubscriber-transact-sql"></a>sp_changesubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改订阅服务器的选项。 更新针对此发布服务器的订阅服务器的任何分发任务。 此存储的过程写入**MSsubscriber_info**分发数据库中的表。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @subscriber = ] 'subscriber'` 是要更改的选项的订阅服务器的名称。 *订阅服务器上*是**sysname**，无默认值。  
  
`[ @type = ] type` 是订阅服务器类型。 *类型*是**tinyint**，默认值为 NULL。 **0**指示[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。 **1**指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或其他 ODBC 数据源服务器订阅服务器。  
  
`[ @login = ] 'login'` 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证登录 id。 login 的数据类型为 sysname，默认值为 NULL   。  
  
`[ @password = ] 'password'` 是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证密码。 *密码*是**sysname**，默认值为 **%** 。 **%** 指示未更改密码属性。  
  
`[ @commit_batch_size = ] commit_batch_size` 支持向后兼容性。  
  
`[ @status_batch_size = ] status_batch_size` 支持向后兼容性。  
  
`[ @flush_frequency = ] flush_frequency` 支持向后兼容性。  
  
`[ @frequency_type = ] frequency_type` 安排分发任务的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|按需|  
|**4**|每天|  
|**8**|每周|  
|**16**|每月|  
|**32**|与“每月”选项相关|  
|**64**|自动启动|  
|**128**|重复执行|  
  
`[ @frequency_interval = ] frequency_interval` 间隔。 *frequency_type*。 *frequency_interval*是**int**，默认值为 NULL。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 是分发任务的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 是在定义重复发生分发任务的频率*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 NULL。  
  
`[ @frequency_subday = ] frequency_subday` 是如何通常定义的周期内重新计划。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 间隔。 *frequence_subday*。 *frequency_subday_interval*是**int**，默认值为 NULL。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 是第一个分发任务时的时间安排，格式为 HHMMSS。 *active_start_time_of_day* 是 **int**，默认值为 NULL。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 是的停止分发任务的时间安排，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 NULL。  
  
`[ @active_start_date = ] active_start_date` 是第一个分发任务的日期安排，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 NULL。  
  
`[ @active_end_date = ] active_end_date` 是正在计划分发任务停止的日期格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 NULL。  
  
`[ @description = ] 'description'` 是一个可选文本说明。 *描述*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ @security_mode = ] security_mode` 是实现的安全模式。 *security_mode*是**int**，可以是下列值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证|  
|**1**|Windows 身份验证|  
  
`[ @publisher = ] 'publisher'` 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*在更改项目属性时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_changesubscriber**用于所有类型的复制。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_changesubscriber**。  
  
## <a name="see-also"></a>请参阅  
 [sp_addsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpdistributiondb (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_helpsubscriberinfo (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
