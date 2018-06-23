---
title: 复制队列读取器代理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- agents [SQL Server replication], Queue Reader Agent
- command prompt [SQL Server replication]
- Queue Reader Agent, parameter reference
- Queue Reader Agent, executables
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
caps.latest.revision: 35
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 84fd65a92213b18dfa7bf8fb85d6ca6dbe66322c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125839"
---
# <a name="replication-queue-reader-agent"></a>复制队列读取器代理
  复制队列读取器代理是一个可执行文件，该文件读取存储在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 队列或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 消息队列中的消息，然后将这些消息应用于发布服务器。 队列读取器代理与允许排队更新的快照发布和事务发布一起使用。  
  
> [!NOTE]  
>  可以按任意顺序指定参数。 如果没有指定可选参数，会使用基于默认代理配置文件的预定义值。  
  
## <a name="syntax"></a>语法  
  
```  
  
      qrdrsvc [-?]  
[-Continuous]  
[-DefinitionFiledefinition_file]  
[-Distributorserver_name[\instance_name]]  
[-DistributionDBdistribution_database]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-LoginTimeOutlogin_time_out_seconds]  
[-Outputoutput_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PollingIntervalpolling_interval]  
[-PublisherFailoverPartnerserver_name[\instance_name] ]  
[-ProfileNameagent_profile_name]  
[-QueryTimeOutquery_time_out_seconds]  
[-ResolverState [1|2|3]]  
```  
  
## <a name="arguments"></a>参数  
 **-?**  
 显示使用信息。  
  
 **-Continuous**  
 指定代理是否尝试连续处理排队的事务。 如果指定此参数，即使任何订阅方都没有挂起的排队事务，代理仍然会连续执行。  
  
 **-DefinitionFile** *def_path_and_file_name*  
 代理定义文件的路径。 代理定义文件中包含代理的命令提示符参数。 文件的内容被当作可执行文件进行分析。 使用双引号 (") 指定包含任意字符的参数值。  
  
 **-Distributor** *server_name*[**\\***instance_name*]  
 分发服务器名称。 为该服务器上的 *默认实例指定* server_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 为该服务器上的 *server_name*\\*instance_name* instance_name [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 。 如果未指定，则名称默认为本地计算机上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的默认实例的名称。  
  
 **-DistributionDB** *distribution_database*  
 分发数据库。  
  
 **-DistributorLogin** *distributor_login*  
 分发服务器登录名。  
  
 **-DistributorPassword** *distributor_password*  
 分发服务器密码。  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 指定分发服务器的安全模式。 值 **0** 指示 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证模式（默认设置），值 **1** 指示 Windows 身份验证模式。  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 队列读取器代理建立连接时使用的安全套接字层 (SSL) 加密级别。  
  
|EncryptionLevel 值|Description|  
|---------------------------|-----------------|  
|**0**|指定不使用 SSL。|  
|**1**|指定使用 SSL，但是代理不验证 SSL 服务器证书是否已由可信的颁发者进行签名。|  
|**2**|指定使用 SSL，并验证证书。|  
  
 有关详细信息，请参阅[安全性概述（复制）](../security/security-overview-replication.md)。  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 指定队列读取器运行期间记录的历史记录数量。 选择 **1**可将历史日志记录对性能的影响减至最小。  
  
|HistoryVerboseLevel 值|Description|  
|-------------------------------|-----------------|  
|**0**|不记录历史记录（不推荐）。|  
|**1**|默认值。 总是更新具有相同状态（启动、进行中、成功等）的上一历史记录消息。 如果不存在状态相同的上一记录，将插入新记录。|  
|**2**|插入新的历史记录，包括空闲消息或长时间运行作业的消息。|  
|**3**|插入包括了可能对排除故障有用的其他详细信息的新历史记录。|  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 登录超时前等待的秒数。默认值为 15 秒。  
  
 **-Output** *output_path_and_file_name*  
 代理输出文件的路径。 如果未提供文件名，则向控制台发送该输出。 如果指定的文件名已存在，会将输出追加到该文件。  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 指定输出是否应提供详细内容。 如果详细级别为 0，则只输出错误消息。 如果详细级别为 1，则输出所有进度报告消息。  如果详细级别为 2（默认），则输出所有错误消息和进度消息，这对调试很有帮助。  
  
 **-PollingInterval** *polling_interval*  
 仅与使用基于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 的队列的更新订阅有关。 指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 队列接受对挂起的排队事务的轮询的频率（以秒为单位）。 该值可介于 0 和 240 秒之间。 默认值为 5 秒。  
  
 **-PublisherFailoverPartner** *server_name*[**\\***instance_name*]  
 指定参加与发布数据库进行的数据库镜像会话的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 故障转移伙伴实例。 有关详细信息，请参阅[数据库镜像和复制 (SQL Server)](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md)。  
  
 **-ProfileName** *agent_profile_name*  
 用于向代理提供一组默认值的代理配置文件的名称。 有关信息，请参阅[复制代理配置文件](replication-agent-profiles.md)。  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 查询超时前等待的秒数。默认值为 1800 秒。  
  
 **-ResolverState** [ **1**| **2**| **3**]  
 指定解决排队更新冲突的方式。 值为 **1** ，表示发布服务器赢得冲突且当前发生冲突的排队事务将在发布服务器和发起更新的订阅服务器上回滚，后续排队事务的处理过程将继续进行。 值为 **2** 表示订阅服务器赢得冲突且排队事务将覆盖发布服务器上的值。 值为 **3** 表示任何冲突都将导致订阅服务器重新初始化；发布服务器赢得冲突，后续排队事务的处理过程将终止且订阅将重新初始化。 事务发布的默认设置为 **1** ，快照发布的默认设置为 **3** 。  
  
## <a name="remarks"></a>Remarks  
 若要启动队列读取器代理，请从命令提示符下执行 **qrdrsvc.exe** 。 有关信息，请参阅 [复制代理可执行文件](../concepts/replication-agent-executables-concepts.md)。  
  
## <a name="see-also"></a>请参阅  
 [复制代理管理](replication-agent-administration.md)  
  
  