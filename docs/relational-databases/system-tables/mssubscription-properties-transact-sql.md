---
title: "MSsubscription_properties (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSsubscription_properties
- MSsubscription_properties_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscription_properties system table
ms.assetid: f96fc1ae-b798-4b05-82a7-564ae6ef23b8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0811b4b8705fda92ff57e782d04f6543b9fd1ebb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssubscriptionproperties-transact-sql"></a>MSsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSsubscription_properties**表包含在订阅服务器上运行复制代理所需的参数信息的行。 对于请求订阅，该表存储在订阅服务器的订阅数据库中；对于推送订阅，该表存储在分发服务器的分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**发布服务器**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布服务器数据库的名称。|  
|**发布**|**sysname**|发布的名称。|  
|**publication_type**|**int**|发布类型：<br /><br /> **0** = 事务。<br /><br /> **2** = 合并。|  
|**publisher_login**|**sysname**|发布服务器上用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录 ID。|  
|**publisher_password**|**nvarchar(524)**|发布服务器上用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的密码（已加密）。|  
|**publisher_security_mode**|**int**|在发布服务器上实现的安全模式：<br /><br /> **0**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] SQL Server 身份验证。<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 身份验证。<br /><br /> **2** = 同步触发器使用静态**sysservers**条目以执行远程过程调用 (RPC)、 和*发布服务器*中必须定义**sysservers**作为远程服务器或链接的服务器的表。|  
|**分发服务器**|**sysname**|分发服务器的名称。|  
|**distributor_login**|**sysname**|在分发服务器用于 SQL Server 身份验证的登录 ID。|  
|**distributor_password**|**nvarchar(524)**|分发服务器上用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的密码（加密）。|  
|**distributor_security_mode**|**int**|在分发服务器上实现的安全模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。<br /><br /> **1** = Windows 身份验证。|  
|**ftp_address**|**sysname**|文件传输协议 (FTP) 服务分发服务器网络地址。|  
|**ftp_port**|**int**|分发服务器的 FTP 服务的端口号。|  
|**ftp_login**|**sysname**|用于连接到 FTP 服务的用户名。|  
|**ftp_password**|**nvarchar(524)**|用于连接到 FTP 服务的 u.User 密码。|  
|**alt_snapshot_folder**|**nvarchar(255)**|指定快照的备用文件夹的位置。|  
|**working_directory**|**nvarchar(255)**|用于存储数据和架构文件的工作目录的名称。|  
|**use_ftp**|**bit**|指定使用 FTP 而非常规协议检索快照。 如果**1**，使用 FTP。|  
|**dts_package_name**|**sysname**|指定 Data Transformation Services (DTS) 包的名称。|  
|**dts_package_password**|**nvarchar(524)**|指定包上的密码。|  
|**dts_package_location**|**int**|存储 DTS 包的位置。|  
|**enabled_for_syncmgr**|**bit**|指定能否通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 同步管理器同步订阅。<br /><br /> **0** = 订阅未注册使用同步管理器。<br /><br /> **1** = 订阅注册使用同步管理器，并可同步而无需启动[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。|  
|**offload_agent**|**bit**|指定是否可以远程或不激活代理。 如果**0**，代理不能远程激活。|  
|**offload_server**|**sysname**|指定用于远程激活的服务器所在的网络的名称。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|指定保存快照文件的文件夹的路径。|  
|**use_web_sync**|**bit**|指定能否通过 HTTP 同步订阅。 值为**1**意味着是否启用了此功能。|  
|**internet_url**|**nvarchar(260)**|表示 Web 同步的复制侦听器所在位置的 URL。|  
|**internet_login**|**sysname**|合并代理连接到承载 Web 同步使用的 Web 服务器时使用的登录名[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。|  
|**internet_password**|**nvarchar(524)**|合并代理连接到承载 Web 同步使用的 Web 服务器时使用的登录名的密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。|  
|**internet_security_mode**|**int**|连接到承载 Web 同步，其中的一个值的 Web 服务器时使用的身份验证模式**1**意味着 Windows 身份验证，并且值为**0**意味着[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证。|  
|**internet_timeout**|**int**|表示 Web 同步请求在多长时间之后过期的时间长度（秒）。|  
|**主机名**|**sysname**|指定的值**HOST_NAME**当在中使用此函数**其中**的联接筛选器或逻辑记录关系子句。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 &#40;Transact SQL &#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_helppullsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)   
 [sp_helpsubscription_properties (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)  
  
  
