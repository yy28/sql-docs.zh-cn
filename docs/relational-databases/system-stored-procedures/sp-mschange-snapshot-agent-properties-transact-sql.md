---
title: sp_MSchange_snapshot_agent_properties (TRANSACT-SQL) |Microsoft Docs
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
- sp_MSchange_snapshot_agent_properties_TSQL
- sp_MSchange_snapshot_agent_properties
helpviewer_keywords:
- sp_MSchange_snapshot_agent_properties
ms.assetid: 7947a788-3fd7-469f-84db-b03ba89a153c
caps.latest.revision: 20
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 67bd8a178ba3e7759257567fdb46af6ddd79daa4
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43019676"
---
# <a name="spmschangesnapshotagentproperties-transact-sql"></a>sp_MSchange_snapshot_agent_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改在运行快照代理作业的属性[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本分发服务器。 此存储的过程用于更改属性，发布服务器上运行的实例上时[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]。 此存储过程在分发服务器上对分发数据库执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_MSchange_snapshot_agent_properties [ @publisher = ] 'publisher'  
        , [ @publisher_db = ] 'publisher_db'  
        , [ @publication = ] 'publication'   
        , [ @frequency_type= ] frequency_type  
        , [ @frequency_interval= ] frequency_interval  
        , [ @frequency_subday= ] frequency_subday  
        , [ @frequency_subday_interval= ] frequency_subday_interval  
        , [ @frequency_relative_interval= ] frequency_relative_interval  
        , [ @frequency_recurrence_factor= ] frequency_recurrence_factor  
        , [ @active_start_date= ] active_start_date  
        , [ @active_end_date= ] active_end_date  
        , [ @active_start_time_of_day= ] active_start_time_of_day  
        , [ @active_end_time_of_day= ] active_end_time_of_day  
        , [ @snapshot_job_name = ] 'snapshot_agent_name'  
        , [ @publisher_security_mode = ] publisher_security_mode  
        , [ @publisher_login = ] 'publisher_login'  
        , [ @publisher_password = ] 'publisher_password'   
        , [ @job_login = ] 'job_login'  
        , [ @job_password = ] 'job_password'  
        , [ @publisher_type = ] 'publisher_type'  
```  
  
## <a name="arguments"></a>参数  
 [ **@publisher** = ] **'***publisher***'**  
 发布服务器的名称。 *发布服务器*是**sysname**，无默认值。  
  
 [  **@publisher_db=** ] **'***publisher_db*****  
 发布数据库的名称。 *publisher_db*是**sysname**，无默认值。  
  
 [ **@publication =** ] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@frequency_type =** ] *frequency_type*  
 执行快照代理的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|按需|  
|**4**|每天|  
|**8**|每周|  
|**10**|每月|  
|**20**|每月，相对于频率间隔|  
|**40**|当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启动时|  
  
 [  **@frequency_interval =** ] *frequency_interval*  
 是要将应用于设置频率的值*frequency_type*。 *frequency_interval*是**int**，无默认值。  
  
 [  **@frequency_subday =** ] *frequency_subday*  
 单位。 *freq_subday_interval*。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4**|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，无默认值。  
  
 [  **@frequency_relative_interval =** ] *frequency_relative_interval*  
 快照代理运行的日期。 *frequency_relative_interval*是**int**，无默认值。  
  
 [  **@frequency_recurrence_factor =** ] *frequency_recurrence_factor*  
 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，无默认值。  
  
 [ **@active_start_date =** ] *active_start_date*  
 第一次安排快照代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，无默认值。  
  
 [ **@active_end_date =** ] *active_end_date*  
 停止安排快照代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，无默认值。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排快照代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，无默认值。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排快照代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，无默认值。  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name*****  
 使用现有作业时现有快照代理作业的名称。 *snapshot_agent_name*是**nvarchar(100)**，无默认值。  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 连接到发布服务器时代理所使用的安全模式。 *publisher_security_mode*是**int**，无默认值。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，并**1**指定 Windows 身份验证。 值为**0**必须为指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login*****  
 连接到发布服务器时所使用的登录名。 *publisher_login*是**sysname**，无默认值。 *publisher_login*时，必须指定*publisher_security_mode*是**0**。 如果*publisher_login*为 NULL，并且发布者 *_ * * security_mode*是**1**，然后在指定的 Windows 帐户*job_login*将连接到发布服务器时使用。  
  
 [ **@publisher_password**=] **'***publisher_password*****  
 连接到发布服务器时所使用的密码。 *publisher_password*是**nvarchar(524)**，无默认值。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为了提高安全性，建议您在运行时提供登录名和密码。  
  
 [ **@job_login**=] **'***job_login*****  
 用于运行代理的 Windows 帐户的登录名。 *job_login*是**nvarchar(257)**，无默认值。 此 Windows 帐户总是用于与分发服务器建立代理连接。 创建新的快照代理作业时，必须提供此参数。 *这是无法更改为非*[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *发布服务器。*  
  
 [ **@job_password**=] **'***job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。 创建新的快照代理作业时，必须提供此参数。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为了提高安全性，建议您在运行时提供登录名和密码。  
  
 [ **@publisher_type**=] **'***publisher_type*****  
 当发布服务器未在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例中运行时指定该发布服务器类型。 *publisher_type*是**sysname**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**|指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。|  
|**ORACLE**|指定标准的 Oracle 发布服务器。|  
|**ORACLE 网关**|指定 Oracle 网关发布服务器。|  
  
 有关 Oracle 发布服务器和 Oracle 网关发布服务器之间的差异的详细信息，请参阅[Oracle 发布概述](../../relational-databases/replication/non-sql/oracle-publishing-overview.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 **sp_MSchange_snapshot_agent_properties**快照复制、 事务复制和合并复制中使用。  
  
 执行时，必须指定所有参数**sp_MSchange_snapshot_agent_properties**。 执行[sp_helppublication_snapshot](../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md)返回快照代理作业的当前属性。  
  
 发布服务器实例上的运行时[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]或更高版本，应使用[sp_changepublication_snapshot](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)若要更改快照代理作业的属性。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**分发服务器上的固定的服务器角色可以执行**sp_MSchange_snapshot_agent_properties**。  
  
## <a name="see-also"></a>请参阅  
 [sp_addpublication_snapshot (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
  
