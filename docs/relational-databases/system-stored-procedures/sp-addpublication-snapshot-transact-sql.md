---
title: sp_addpublication_snapshot (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_addpublication_snapshot_TSQL
- sp_addpublication_snapshot
helpviewer_keywords:
- sp_addpublication_snapshot
ms.assetid: 192b6214-df6e-44a3-bdd4-9d933a981619
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7a56fad97e7716cce4cc52858b6af2b24a6e09a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731055"
---
# <a name="spaddpublicationsnapshot-transact-sql"></a>sp_addpublication_snapshot (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  为指定的发布创建快照代理。 在发布服务器上对发布数据库执行此存储的过程。  
  
> [!IMPORTANT]  
>  使用远程分发服务器配置发布服务器时，为所有参数提供的值（包括 *job_login* 和 *job_password*）都会以纯文本方式发送到该分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addpublication_snapshot [ @publication= ] 'publication'  
    [ , [ @frequency_type= ] frequency_type ]  
    [ , [ @frequency_interval= ] frequency_interval ]  
    [ , [ @frequency_subday= ] frequency_subday ]  
    [ , [ @frequency_subday_interval= ] frequency_subday_interval ]  
    [ , [ @frequency_relative_interval= ] frequency_relative_interval ]  
    [ , [ @frequency_recurrence_factor= ] frequency_recurrence_factor ]  
    [ , [ @active_start_date= ] active_start_date ]  
    [ , [ @active_end_date= ] active_end_date ]  
    [ , [ @active_start_time_of_day= ] active_start_time_of_day ]  
    [ , [ @active_end_time_of_day= ] active_end_time_of_day ]  
    [ , [ @snapshot_job_name = ] 'snapshot_agent_name' ]  
    [ , [ @publisher_security_mode = ] publisher_security_mode ]  
    [ , [ @publisher_login = ] 'publisher_login' ]  
    [ , [ @publisher_password = ] 'publisher_password' ]   
    [ , [ @job_login = ] 'job_login' ]  
    [ , [ @job_password = ] 'job_password' ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@frequency_type=**] *frequency_type*  
 执行快照代理的频率。 *frequency_type*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次。|  
|**4** （默认值）|每天。|  
|**8**|每周。|  
|**16**|每月。|  
|**32**|每月，相对于频率间隔。|  
|**64**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理启动时。|  
|**128**|计算机空闲时运行|  
  
 [  **@frequency_interval=**] *frequency_interval*  
 是要将应用于设置频率的值*frequency_type*。 *frequency_interval*是**int**，可以是下列值之一。  
  
|frequency_type 的值|对 frequency_interval 的影响|  
|------------------------------|-----------------------------------|  
|**1**|*frequency_interval*是未使用。|  
|**4** （默认值）|每个*frequency_interval*天，默认值为每日。|  
|**8**|*frequency_interval*是一个或多个以下 (结合[ &#124; （位或）](../../t-sql/language-elements/bitwise-or-transact-sql.md)逻辑运算符):<br /><br /> **1** = 星期日&#124;<br /><br /> **2** = 星期一&#124;<br /><br /> **4** = 星期二&#124;<br /><br /> **8** = 星期三&#124;<br /><br /> **16** = 星期四&#124;<br /><br /> **32** = 星期五&#124;<br /><br /> **64** = 星期六|  
|**16**|上*frequency_interval*天的月份。|  
|**32**|*frequency_interval*是以下之一：<br /><br /> **1** = 星期日&#124;<br /><br /> **2** = 星期一&#124;<br /><br /> **3** = 星期二&#124;<br /><br /> **4** = 星期三&#124;<br /><br /> **5** = 星期四&#124;<br /><br /> **6** = 星期五&#124;<br /><br /> **7** = 星期六&#124;<br /><br /> **8** = 天&#124;<br /><br /> **9** = 工作日&#124;<br /><br /> **10** = 休息日|  
|**64**|*frequency_interval*是未使用。|  
|**128**|*frequency_interval*是未使用。|  
  
 [  **@frequency_subday=**] *frequency_subday*  
 是的单位*freq_subday_interval*。 *frequency_subday*是**int**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|一次|  
|**2**|第二个|  
|**4** （默认值）|Minute|  
|**8**|Hour|  
  
 [  **@frequency_subday_interval=**] *frequency_subday_interval*  
 间隔。 *frequency_subday*。 *frequency_subday_interval*是**int**，默认值为 5，这意味着每隔 5 分钟。  
  
 [  **@frequency_relative_interval=**] *frequency_relative_interval*  
 快照代理运行的日期。 *frequency_relative_interval*是**int**，默认值为 1。  
  
 [  **@frequency_recurrence_factor=**] *frequency_recurrence_factor*  
 使用的重复因子*frequency_type*。 *frequency_recurrence_factor*是**int**，默认值为 0。  
  
 [  **@active_start_date=**] *active_start_date*  
 第一次安排快照代理的日期，格式为 YYYYMMDD。 *active_start_date*是**int**，默认值为 0。  
  
 [  **@active_end_date=**] *active_end_date*  
 停止安排快照代理的日期，格式为 YYYYMMDD。 *active_end_date*是**int**，默认值为 99991231，表示年 12 月 31 日到 9999。  
  
 [  **@active_start_time_of_day=**] *active_start_time_of_day*  
 第一次安排快照代理的时间，格式为 HHMMSS。 *active_start_time_of_day*是**int**，默认值为 0。  
  
 [  **@active_end_time_of_day=**] *active_end_time_of_day*  
 停止安排快照代理的时间，格式为 HHMMSS。 *active_end_time_of_day*是**int**，默认值为 235959，表示 11:59:59 PM 24 小时制。  
  
 [  **@snapshot_job_name =** ] **'***snapshot_agent_name*****  
 使用现有作业时现有快照代理作业的名称。 *snapshot_agent_name*是**nvarchar(100)** 默认值为 NULL。 此参数只限内部使用，创建新发布时不应指定它。 如果*snapshot_agent_name*指定了，则*job_login*并*job_password*必须为 NULL。  
  
 [ **@publisher_security_mode**=] *publisher_security_mode*  
 连接到发布服务器时代理所使用的安全模式。 *publisher_security_mode*是**smallint**，默认值为 1。 **0**指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证，并**1**指定 Windows 身份验证。 值为**0**必须为指定非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 [ **@publisher_login**=] **'***publisher_login*****  
 连接到发布服务器时所使用的登录名。 *publisher_login*是**sysname**，默认值为 NULL。 *publisher_login*时，必须指定*publisher_security_mode*是**0**。 如果*publisher_login*为 NULL 并*publisher_security_mode*是**1**，然后在指定的帐户*job_login*时要使用连接到发布服务器。  
  
 [ **@publisher_password**=] **'***publisher_password*****  
 连接到发布服务器时所使用的密码。 *publisher_password*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为了提高安全性，建议您在运行时提供登录名和密码。  
  
 [ **@job_login**=] **'***job_login*****  
 是用于运行代理的帐户的登录名。 在 Azure SQL 数据库托管实例，使用 SQL Server 帐户。 *job_login*是**nvarchar(257)**，默认值为 NULL。 此帐户始终用于到分发服务器的代理连接。 创建新的快照代理作业时，必须提供此参数。  
  
> [!NOTE]  
>  对于非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器，这必须是相同的登录名中指定[sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)。  
  
 [ **@job_password**=] **'***job_password*****  
 用于运行代理的 Windows 帐户的密码。 *job_password*是**sysname**，无默认值。 创建新的快照代理作业时，必须提供此参数。  
  
> [!IMPORTANT]  
>  请不要将身份验证信息存储在脚本文件中。 为了提高安全性，建议您在运行时提供登录名和密码。  
  
 [ **@publisher**=] **'***发布服务器*****  
 指定非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*创建中的快照代理时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addpublication_snapshot**快照复制、 事务复制和合并复制中使用。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranPub](../../relational-databases/replication/codesnippet/tsql/sp-addpublication-snapsh_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addpublication_snapshot**。  
  
## <a name="see-also"></a>请参阅  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [创建并应用快照](../../relational-databases/replication/create-and-apply-the-snapshot.md)   
 [sp_addpublication &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)   
 [sp_changepublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)   
 [sp_startpublication_snapshot &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-startpublication-snapshot-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
