---
title: "sp_helpsubscription_properties (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpsubscription_properties
- sp_helpsubscription_properties_TSQL
helpviewer_keywords:
- sp_helpsubscription_properties
ms.assetid: 7a76a645-97eb-47ac-b3ea-e2d75012cbed
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 060aad04898e9ce47c91cf835b107e4c2efc39e3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpsubscriptionproperties-transact-sql"></a>sp_helpsubscription_properties (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  检索安全信息从[MSsubscription_properties](../../relational-databases/system-tables/mssubscription-properties-transact-sql.md)表。 此存储过程在订阅服务器上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpsubscription_properties [ [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db =] 'publisher_db' ]   
    [ , [ @publication =] 'publication' ]  
    [ , [ @publication_type = ] publication_type ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@publisher=**] *发布服务器*  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 **%** ，它返回所有发布服务器上的信息。  
  
 [  **@publisher_db=**] *publisher_db*  
 发布服务器数据库的名称。 *publisher_db*是**sysname**，默认值为 **%** ，它返回所有发布服务器数据库上的信息。  
  
 [  **@publication=**] *发布*  
 发布的名称。 *发布*是**sysname**，默认值为 **%** ，其返回有关所有发布的信息。  
  
 [  **@publication_type=**] *publication_type*  
 是的类型。*publication_type*是**int**，默认值为 NULL。 如果提供， *publication_type*必须是以下值之一：  
  
|值|说明|  
|-----------|-----------------|  
|**0**|事务发布|  
|**1**|快照发布|  
|**2**|合并发布|  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**发布服务器**|**sysname**|发布服务器的名称。|  
|**publisher_db**|**sysname**|发布服务器数据库名。|  
|**发布**|**sysname**|发布的名称。|  
|**publication_type**|**int**|发布的类型：<br /><br /> **0** = 事务<br /><br /> **1** = 快照<br /><br /> **2** = 合并|  
|**publisher_login**|**sysname**|在发布服务器上用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证的登录 ID。|  
|**publisher_password**|**nvarchar(524)**|在发布服务器使用密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（加密） 的身份验证。|  
|**publisher_security_mode**|**int**|发布服务器上使用的安全模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1** = Windows 身份验证|  
|**分发服务器**|**sysname**|分发服务器的名称。|  
|**distributor_login**|**sysname**|分发服务器登录名。|  
|**distributor_password**|**nvarchar(524)**|分发服务器密码（已加密）。|  
|**distributor_security_mode**|**int**|分发服务器上使用的安全模式：<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]身份验证<br /><br /> **1** = Windows 身份验证|  
|**ftp_address**|**sysname**|仅为保持向后兼容。 分发服务器的文件传输协议 (FTP) 服务的网络地址。|  
|**ftp_port**|**int**|仅为保持向后兼容。 分发服务器的 FTP 服务端口号。|  
|**ftp_login**|**sysname**|仅为保持向后兼容。 用于连接到 FTP 服务的用户名。|  
|**ftp_password**|**nvarchar(524)**|仅为保持向后兼容。 用于连接到 FTP 服务的用户密码。|  
|**alt_snapshot_folder**|**nvarchar(255)**|指定快照的备用文件夹的位置。|  
|**working_directory**|**nvarchar(255)**|用于存储数据和架构文件的工作目录的名称。|  
|**use_ftp**|**bit**|指定使用 FTP 而非常规协议检索快照。 如果**1**，使用 FTP。|  
|**dts_package_name**|**sysame**|指定 Data Transformation Services (DTS) 包的名称。|  
|**dts_package_password**|**nvarchar(524)**|指定用于包的密码（如果有）。|  
|**dts_package_location**|**int**|DTS 包的存储位置的位置。<br /><br /> **0** = 包位置为分发服务器。<br /><br /> **1** = 包位置为订阅服务器。|  
|**offload_agent**|**bit**|指定是否可以远程激活代理。 如果**0**，代理不能远程激活。|  
|**offload_server**|**sysname**|指定用于远程激活的服务器所在的网络的名称。|  
|**dynamic_snapshot_location**|**nvarchar(255)**|指定保存快照文件的文件夹的路径。|  
|**use_web_sync**|**bit**|指定其中的一个值，是否可以通过 HTTPS 中, 同步订阅**1**意味着是否启用了此功能。|  
|**internet_url**|**nvarchar(260)**|表示 Web 同步复制侦听器的位置的 URL。|  
|**internet_login**|**nvarchar （128)**|在使用基本身份验证连接到承载 Web 同步的 Web 服务器时，合并代理所使用的登录名。|  
|**internet_password**|**nvarchar(524)**|在使用基本身份验证连接到承载 Web 同步的 Web 服务器时，合并代理所使用的登录密码。|  
|**internet_security_mode**|**int**|连接到承载 Web 同步，其中的一个值的 Web 服务器时使用的身份验证模式**1**意味着 Windows 身份验证，并且值为**0**意味着基本身份验证。|  
|**internet_timeout**|**int**|Web 同步请求过期之前的时间长度（秒）。|  
|**主机名**|**nvarchar （128)**|在 WHERE 子句参数化行筛选器中使用 HOST_NAME() 函数时，指定此函数的值。|  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_helpsubscription_properties**快照复制、 事务复制和合并复制中使用。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_helpsubscription_properties**。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
