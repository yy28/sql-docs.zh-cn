---
title: sys.dm_exec_connections (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_exec_connections_TSQL
- sys.dm_exec_connections_TSQL
- sys.dm_exec_connections
- dm_exec_connections
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_connections dynamic management view
ms.assetid: 6bd46fe1-417d-452d-a9e6-5375ee8690d8
caps.latest.revision: 50
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 0cc531232731aa3e2b2bf29a5538396be06b7e5c
ms.sourcegitcommit: 8b332c12850c283ae413e0b04b2b290ac2edb672
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2018
---
# <a name="sysdmexecconnections-transact-sql"></a>sys.dm_exec_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关与此 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例建立的连接的信息以及每个连接的详细信息。 返回 SQL Server 的 server 宽的连接信息。 返回当前的 SQL 数据库的数据库连接信息。  
  
> [!NOTE]
> 若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用[sys.dm_pdw_exec_connections &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-connections-transact-sql.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|session_id|**int**|标识与此连接关联的会话。 可以为 Null。|  
|most_recent_session_id|**int**|表示与此连接关联的最近请求的会话 ID。 （另一个会话可以重用 SOAP 连接。）可以为 Null。|  
|connect_time|**datetime**|连接建立时的时间戳。 不可为 null。|  
|net_transport|**nvarchar(40)**|始终返回**会话**连接当具有多个活动结果集 (MARS) 启用。<br /><br /> **注意：**描述此连接使用的物理传输协议。 不可为 null。|  
|protocol_type|**nvarchar(40)**|指定负载的协议类型。 此参数当前可区分 TDS (TSQL) 和 SOAP。 可以为 Null。|  
|protocol_version|**int**|与此连接关联的数据访问协议的版本。 可以为 Null。|  
|endpoint_id|**int**|说明其连接类型的标识符。 此 endpoint_id 可用于查询 sys.endpoints 视图。 可以为 Null。|  
|encrypt_option|**nvarchar(40)**|说明是否为此连接启用了加密的布尔值。 不可为 null。|  
|auth_scheme|**nvarchar(40)**|指定此连接使用的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/Windows 身份验证方案。 不可为 null。|  
|node_affinity|**int**|标识与此连接关联的内存节点。 不可为 null。|  
|num_reads|**int**|字节读取已发生的此连接数。 可以为 Null。|  
|num_writes|**int**|通过此连接已发生的字节写入数。 可以为 Null。|  
|last_read|**datetime**|此连接中上一次发生读操作的时间戳。 可以为 Null。|  
|last_write|**datetime**|此连接中上一次发生写操作的时间戳。 不可为 Null。|  
|net_packet_size|**int**|用于信息和数据传输的网络包的大小。 可以为 Null。|  
|client_net_address|**varchar(48)**|与此服务器连接的客户端的主机地址。 可以为 Null。<br /><br /> 在 V12 之前[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，此列始终返回 NULL。|  
|client_tcp_port|**int**|与此连接关联的客户端计算机上的端口号。 可以为 Null。<br /><br /> 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，此列始终返回 NULL。|  
|local_net_address|**varchar(48)**|表示此连接的目标服务器的 IP 地址。 只对使用 TCP 传输提供程序的连接可用。 可以为 Null。<br /><br /> 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，此列始终返回 NULL。|  
|local_tcp_port|**int**|如果此连接使用 TCP 传输，则表示此连接的目标服务器的 TCP 端口。 可以为 Null。<br /><br /> 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，此列始终返回 NULL。|  
|connection_id|**uniqueidentifier**|对每个连接进行唯一标识。 不可为 null。|  
|parent_connection_id|**uniqueidentifier**|标识 MARS 会话正在使用的主要连接。 可以为 Null。|  
|most_recent_sql_handle|**varbinary(64)**|此连接上执行的上一个请求的 SQL 句柄。 most_recent_sql_handle 列始终与 most_recent_session_id 列同步。 可以为 Null。|  
|pdw_node_id|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="physical-joins"></a>物理联接  
 ![有关 sys.dm_exec_connections 联接](../../relational-databases/system-dynamic-management-views/media/join-dm-exec-connections-1.gif "有关 sys.dm_exec_connections 联接")  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
||||  
|-|-|-|  
|dm_exec_sessions.session_id|dm_exec_connections.session_id|一对一|  
|dm_exec_requests.connection_id|dm_exec_connections.connection_id|多对一|  
|dm_broker_connections.connection_id|dm_exec_connections.connection_id|一对一|  
  
## <a name="examples"></a>示例  
 收集查询自有连接有关信息的典型查询。  
  
```sql  
SELECT   
    c.session_id, c.net_transport, c.encrypt_option,   
    c.auth_scheme, s.host_name, s.program_name,   
    s.client_interface_name, s.login_name, s.nt_domain,   
    s.nt_user_name, s.original_login_name, c.connect_time,   
    s.login_time   
FROM sys.dm_exec_connections AS c  
JOIN sys.dm_exec_sessions AS s  
    ON c.session_id = s.session_id  
WHERE c.session_id = @@SPID;  
```  
  
## <a name="see-also"></a>另请参阅  

 [执行相关的动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


