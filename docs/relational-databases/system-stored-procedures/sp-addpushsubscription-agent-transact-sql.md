---
title: sp_addpushsubscription_agent (Transact SQL) |Microsoft 文档
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
- sp_addpushsubscription_agent_TSQL
- sp_addpushsubscription_agent
helpviewer_keywords:
- sp_addpushsubscription_agent
ms.assetid: 1fdd2052-50d8-4318-8aa7-fc635d5cad18
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d111bef33c73d2417ddccf88c5bb083be6c2a35f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993544"
---
# <a name="spaddpushsubscriptionagent-transact-sql"></a>sp_addpushsubscription_agent (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加新的预定代理作业，以使推送订阅与事务发布同步。 在发布服务器的发布数据库上执行此存储的过程。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addpushsubscription_agent [ @publication= ] 'publication'  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @subscriber_db = ] 'subscriber_db' ]  
    [ , [ @subscriber_security_mode = ] subscriber_security_mode ]  
    [ , [ @subscriber_login = ] 'subscriber_login' ]  
    [ , [ @subscriber_password = ] 'subscriber_password' ]  
    [ , [ @job_login = ] 'job_login' ]   
    [ , [ @job_password = ] 'job_password' ]   
    [ , [ @job_name = ] 'job_name' ]   
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
    [ , [ @dts_package_name = ] 'dts_package_name' ]  
    [ , [ @dts_package_password = ] 'dts_package_password' ]  
    [ , [ @dts_package_location = ] 'dts_package_location' ]  
    [ , [ @enabled_for_syncmgr = ] 'enabled_for_syncmgr' ]  
    [ , [ @distribution_job_name = ] 'distribution_job_name' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @subscriber_provider = ] 'subscriber_provider' ]   
    [ , [ @subscriber_datasrc = ] 'subscriber_datasrc' ]   
    [ , [ @subscriber_location = ] 'subscriber_location' ]  
    [ , [ @subscriber_provider_string = ] 'subscriber_provider_string' ]   
    [ , [ @subscriber_catalog = ] 'subscriber_catalog' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication =**] *****发布*****  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@subscriber =**] *****订阅服务器*****  
 订阅服务器的名称。 *订阅服务器*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_db =**] *****subscriber_db*****  
 是订阅数据库的名称。 *subscriber_db*是**sysname**，默认值为 NULL。 对于非 SQL Server 订阅服务器，指定的值 **（默认目标）** 为*subscriber_db*。  
  
 [  **@subscriber_security_mode =**] *subscriber_security_mode*  
 同步时连接到订阅服务器所使用的安全模式。 *subscriber_security_mode*是**int**，默认值为 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。 **1**指定 Windows 身份验证。  
  
> [!IMPORTANT]  
>  对于在队列中排队的更新订阅，请将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 验证用于与订阅服务器的连接，并为每个订阅服务器连接指定一个不同的帐户。 对于所有其他订阅，则使用 Windows 身份验证。  
  
 [  **@subscriber_login =**] *****subscriber_login*****  
 同步时连接到订阅服务器所使用的订阅服务器登录。 *subscriber_login*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_password =**] *****subscriber_password*****  
 订阅服务器密码。 *subscriber_password*是必需的如果*subscriber_security_mode*设置为**0**。 *subscriber_password*是**sysname**，默认值为 NULL。 如果使用订阅服务器密码，将自动对密码进行加密。  
  
> [!IMPORTANT]  
>  不要使用空密码。 请使用强密码。 如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [  **@job_login =** ] *****job_login*****  
 用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)**，默认值为 NULL。 使用 Windows 集成身份验证时，此 Windows 帐户始终用于代理与分发服务器的连接，以及与订阅服务器的连接。  
  
 [  **@job_password =** ] *****job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
 [ **@job_name =** ] **'***job_name***'**  
 现有代理作业的名称。 *job_name*是**sysname**，默认值为 NULL。 只有在使用现有作业而不是新创建的作业（此为默认设置）来同步订阅时，才需要指定此参数。 如果你不属于**sysadmin**固定服务器角色，你必须指定*job_login*和*job_password*时指定*job_name*.  
  
 [  **@frequency_type =** ] *frequency_type*  
 安排分发代理计划的频率。 *frequency_type*是**int**，和可以是以下值之一。  
  
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
>  指定的值**64**导致分发代理以连续模式运行。 这对应于设置 **-连续**代理程序的参数。 有关详细信息，请参阅 [Replication Distribution Agent](../../relational-databases/replication/agents/replication-distribution-agent.md)。  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 是要应用于通过设置的频率的值*frequency_type*。 *frequency_interval*是**int**，默认值为 1。  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 分发代理的日期。 使用此参数时*frequency_type*设置为**32** （每月相对）。 *frequency_relative_interval*是**int**，和可以是以下值之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|**1** （默认值）|第一个|  
|**2**|第二个|  
|**4**|第三个|  
|**8**|第四个|  
|**16**|上一次|  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 是由重复因素*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 0。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 在指定期内重新安排计划的频率。 *frequency_subday*是**int**，和可以是以下值之一。  
  
|“值”|说明|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4** （默认值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval =** ] *frequency_subday_interval*  
 是的间隔*frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 5。  
  
 [  **@active_start_time_of_day =** ] *active_start_time_of_day*  
 第一次安排分发代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 0。  
  
 [  **@active_end_time_of_day =** ] *active_end_time_of_day*  
 停止安排分发代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 235959。  
  
 [ **@active_start_date =** ] *active_start_date*  
 第一次安排分发代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 0。  
  
 [ **@active_end_date =** ] *active_end_date*  
 停止安排分发代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 99991231。  
  
 [  **@dts_package_name =** ] *****dts_package_name*****  
 指定 Data Transformation Services (DTS) 包的名称。 *dts_package_name*是**sysname**默认值为 NULL。 例如，若要指定的包名称`DTSPub_Package`，则参数应为`@dts_package_name = N'DTSPub_Package'`。  
  
 [  **@dts_package_password =** ] *****dts_package_password*****  
 指定运行包所需的密码。 *dts_package_password*是**sysname**默认值为 NULL。  
  
> [!NOTE]  
>  如果满足以下条件，则必须指定密码*dts_package_name*指定。  
  
 [  **@dts_package_location =** ] *****dts_package_location*****  
 指定包位置。 *dts_package_location*是**nvarchar(12)**，默认值为分发服务器。 包的位置可以是**分发服务器**或**订阅服务器**。  
  
 [  **@enabled_for_syncmgr =** ] *****enabled_for_syncmgr*****  
 是是否通过同步订阅[!INCLUDE[msCoName](../../includes/msconame-md.md)]同步管理器。 *enabled_for_syncmgr*是**nvarchar(5)**，默认值为 FALSE。 如果**false**，订阅未注册使用同步管理器。 如果**true**，该订阅已注册使用同步管理器，可以同步而无需启动[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
 [  **@distribution_job_name =** ] *****distribution_job_name*****  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@publisher =** ] *****发布服务器*****  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。  
  
 [  **@subscriber_provider=** ] *****subscriber_provider*****  
 非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的 OLE DB 访问接口注册时使用的唯一编程标识符 (PROGID)。 *subscriber_provider*是**sysname**，默认值为 NULL。 *subscriber_provider*必须是唯一的分发服务器上安装的 OLE DB 提供程序。 *subscriber_provider*仅支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
 [  **@subscriber_datasrc=** ] *****subscriber_datasrc*****  
 为已理解 OLE DB 访问接口是数据源的名称。 *subscriber_datasrc*是**nvarchar （4000)**，默认值为 NULL。 *subscriber_datasrc*作为要初始化的 OLE DB 访问接口的 DBPROP_INIT_DATASOURCE 属性传递。 *subscriber_datasrc*仅支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
 [  **@subscriber_location=** ] *****subscriber_location*****  
 OLE DB 访问接口所了解的数据库的位置。 *subscriber_location*是**nvarchar （4000)**，默认值为 NULL。 *subscriber_location*作为要初始化的 OLE DB 访问接口的 DBPROP_INIT_LOCATION 属性传递。 *subscriber_location*仅支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
 [  **@subscriber_provider_string=** ] *****subscriber_provider_string*****  
 用于标识数据源的特定于 OLE DB 访问接口的连接字符串。 *subscriber_provider_string*是**nvarchar （4000)**，默认值为 NULL。 *subscriber_provider_string*被传递给 IDataInitialize 或设置作为 DBPROP_INIT_PROVIDERSTRING 属性为初始化 OLE DB 提供程序。 *subscriber_provider_string*仅支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
 [  **@subscriber_catalog=** ] *****subscriber_catalog*****  
 连接到 OLE DB 访问接口时使用的目录。 *subscriber_catalog*是**sysname**，默认值为 NULL。 *subscriber_catalog*作为要初始化的 OLE DB 访问接口的 DBPROP_INIT_CATALOG 属性传递。 *subscriber_catalog*仅支持非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]订阅服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addpushsubscription_agent**快照复制和事务复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../relational-databases/replication/codesnippet/tsql/sp-addpushsubscription-a_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addpushsubscription_agent**。  
  
## <a name="see-also"></a>另请参阅  
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [为非 SQL Server 订阅服务器创建订阅](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [复制存储过程 &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sp_addsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)   
 [sp_dropsubscription &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)  
  
  
