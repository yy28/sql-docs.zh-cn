---
title: sp_addsubscriber (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
author: stevestein
ms.author: sstein
ms.openlocfilehash: cb21731dd02fee4ec3779affed56f85e5dbc0e9b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68079232"
---
# <a name="spaddsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向发布服务器添加新的订阅服务器，使其能够接收发布。 对于快照和事务发布，此存储过程在发布服务器的发布数据库中执行；对于使用远程分发服务器的合并发布，此存储过程在分发服务器执行。  
  
> [!IMPORTANT]  
>  已不推荐使用此存储过程。 不再需要显式注册发布服务器上的订阅服务器。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addsubscriber [ @subscriber = ] 'subscriber'  
    [ , [ @type = ] type ]   
    [ , [ @login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @commit_batch_size = ] commit_batch_size ]  
    [ , [ @status_batch_size = ] status_batch_size ]  
    [ , [ @flush_frequency = ] flush_frequency ]  
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
    [ , [ @description = ] 'description' ]  
    [ , [ @security_mode = ] security_mode ]  
    [ , [ @encrypted_password = ] encrypted_password ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @subscriber = ] 'subscriber'` 是要作为有效的订阅服务器添加到此服务器上发布的名称。 *订阅服务器上*是**sysname**，无默认值。  
  
`[ @type = ] type` 是订阅服务器的类型。 *类型*是**tinyint**，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**0** （默认值）|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器|  
|**1**|ODBC 数据源服务器|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 数据库|  
|**3**|OLE DB 访问接口|  
  
`[ @login = ] 'login'` 是的登录名 ID[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 login 的数据类型为 sysname，默认值为 NULL   。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @password = ] 'password'` 是的密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 *密码*是**nvarchar(524)** ，默认值为 NULL。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @commit_batch_size = ] commit_batch_size` 此参数已弃用，为了保持向后兼容性的脚本。  
  
> [!NOTE]  
>  在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @status_batch_size = ] status_batch_size` 此参数已弃用，为了保持向后兼容性的脚本。  
  
> [!NOTE]  
>  在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @flush_frequency = ] flush_frequency` 此参数已弃用，为了保持向后兼容性的脚本。  
  
> [!NOTE]  
>  在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @frequency_type = ] frequency_type` 是用来安排复制代理的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
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
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [ **@frequency_interval=** ] *frequency_interval*  
 是应用于设置频率的值*frequency_type*。 *frequency_interval*是**int**，默认值为 1。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @frequency_relative_interval = ] frequency_relative_interval` 是复制代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，可以是下列值之一。  
  
|ReplTest1|描述|  
|-----------|-----------------|  
|**1** （默认值）|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @frequency_recurrence_factor = ] frequency_recurrence_factor` 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为**0**。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @frequency_subday = ] frequency_subday` 是如何通常定义的周期内重新计划。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4** （默认值）|Minute|  
|**8**|Hour|  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @frequency_subday_interval = ] frequency_subday_interval` 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，默认值为**5**。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @active_start_time_of_day = ] active_start_time_of_day` 是第一个复制代理时的时间安排，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为**0**。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @active_end_time_of_day = ] active_end_time_of_day` 停止复制代理的时间安排，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 235959，表示 11:59:59 PM 24 小时制。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @active_start_date = ] active_start_date` 是第一个复制代理的日期安排，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 0。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @active_end_date = ] active_end_date` 是停止复制代理的日期安排，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 99991231，表示年 12 月 31 日到 9999。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @description = ] 'description'` 是订阅服务器上的文本说明。 *描述*是**nvarchar(255)** ，默认值为 NULL。  
  
`[ @security_mode = ] security_mode` 是实现的安全模式。 *security_mode*是**int**，默认值为 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 **1**指定 Windows 身份验证。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
`[ @encrypted_password = ] encrypted_password` 此参数已弃用，仅设置用于向后兼容性*encrypted_password*的任何值，但**0**将导致错误。  
  
`[ @publisher = ] 'publisher'` 指定一个非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*从发布时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addsubscriber**快照复制、 事务复制和合并复制中使用。  
  
 **sp_addsubscriber**时才会匿名订阅合并发布订阅服务器上不需要。  
  
 **sp_addsubscriber**写入[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)表中**分发**数据库。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_addsubscriber**。  
  
## <a name="see-also"></a>请参阅  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
