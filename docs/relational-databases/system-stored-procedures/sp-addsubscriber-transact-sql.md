---
title: sp_addsubscriber (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_addsubscriber
- sp_addsubscriber_TSQL
helpviewer_keywords:
- sp_addsubscriber
ms.assetid: b8a584ea-2a26-4936-965b-b84f026e39c0
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a78d29cfa36616e1d440295d5ed089d9489ecd31
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993034"
---
# <a name="spaddsubscriber-transact-sql"></a>sp_addsubscriber (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  向发布服务器添加新的订阅服务器，使其能够接收发布。 对于快照和事务发布，此存储过程在发布服务器的发布数据库中执行；对于使用远程分发服务器的合并发布，此存储过程在分发服务器执行。  
  
> [!IMPORTANT]  
>  已不推荐使用此存储过程。 你不再需要显式注册订阅服务器在发布服务器。  
  
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
 [  **@subscriber=**] *****订阅服务器*****  
 将作为有效订阅服务器添加到该服务器的发布中的订阅服务器的名称。 *订阅服务器*是**sysname**，无默认值。  
  
 [  **@type=**]*类型*  
 订阅服务器的类型。 *类型*是**tinyint**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**0** （默认值）|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器|  
|**1**|ODBC 数据源服务器|  
|**2**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Jet 数据库|  
|**3**|OLE DB 访问接口|  
  
 [  **@login=**] *****登录*****  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录 ID。 login 的数据类型为 sysname，默认值为 NULL。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@password=**] *****密码*****  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的密码。 *密码*是**nvarchar(524)**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@commit_batch_size=**] *commit_batch_size*  
 不推荐使用此参数，保留它是为了让脚本能够向后兼容。  
  
> [!NOTE]  
>  在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@status_batch_size=**] *status_batch_size*  
 不推荐使用此参数，保留它是为了让脚本能够向后兼容。  
  
> [!NOTE]  
>  在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@flush_frequency=**] *flush_frequency*  
 不推荐使用此参数，保留它是为了让脚本能够向后兼容。  
  
> [!NOTE]  
>  在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@frequency_type=**] *frequency_type*  
 安排复制代理的频率。 *frequency_type*是**int**，并且可以为这些值之一。  
  
|“值”|说明|  
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
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [**@frequency_interval=** ] *frequency_interval*  
 是应用于通过设置的频率的值*frequency_type*。 *frequency_interval*是**int**，默认值为 1。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 复制代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，并且可以为这些值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**1** （默认值）|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 是由重复因素*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为**0**。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@frequency_subday=**] *frequency_subday*  
 在指定期内重新安排计划的频率。 *frequency_subday*是**int**，并且可以为这些值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4** （默认值）|Minute|  
|**8**|Hour|  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 是的间隔*frequency_subday*。 *frequency_subday_interval*是**int**，默认值为**5**。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排复制代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为**0**。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排复制代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 235959，这意味着 11:59:59 PM 根据在 24 小时制测量值。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@active_start_date=**] *active_start_date*  
 第一次安排复制代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 0。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@active_end_date=**] *active_end_date*  
 停止安排复制代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 99991231，这意味着年 12 月 31 日到 9999。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@description=**] *****说明*****  
 订阅服务器的文本说明。 *说明*是**nvarchar （255)**，默认值为 NULL。  
  
 [  **@security_mode=**] *security_mode*  
 所实现的安全模式。 *security_mode*是**int**，默认值为 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 **1**指定 Windows 身份验证。  
  
> [!NOTE]  
>  不推荐使用此参数，保留它是为了让脚本能够向后兼容。 在执行时现在基于每个订阅指定的属性[sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 在指定值后，该值将用作在此订阅服务器上创建订阅时的默认值，同时返回一条警告消息。  
  
 [  **@encrypted_password=**] *encrypted_password*  
 此参数已弃用，因此仅设置为向后兼容性提供*encrypted_password*为任何值，但**0**将导致错误。  
  
 [ **@publisher**=] *****发布服务器*****  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*从发布时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addsubscriber**快照复制、 事务复制和合并复制中使用。  
  
 **sp_addsubscriber**订阅服务器将仅具有匿名订阅合并发布时不需要。  
  
 **sp_addsubscriber**写入[MSsubscriber_info](../../relational-databases/system-tables/mssubscriber-info-transact-sql.md)表中**分发**数据库。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色可以执行**sp_addsubscriber**。  
  
## <a name="see-also"></a>另请参阅  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [创建请求订阅](../../relational-databases/replication/create-a-pull-subscription.md)   
 [sp_changesubscriber &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md)   
 [sp_dropsubscriber &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscriber-transact-sql.md)   
 [sp_helpsubscriberinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md)  
  
  
