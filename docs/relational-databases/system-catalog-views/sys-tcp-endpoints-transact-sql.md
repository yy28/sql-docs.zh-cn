---
title: "sys.tcp_endpoints (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.tcp_endpoints
- sys.tcp_endpoints_TSQL
- tcp_endpoints
- tcp_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.tcp_endpoints catalog view
ms.assetid: 43cc3afa-cced-4463-8e97-fbfdaf2e4fa8
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2be15d96b5ab7274688c34303ccf1603064dce9d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="systcpendpoints-transact-sql"></a>sys.tcp_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  系统中的每个 TCP 端点都对应一行。 描述了终结点**sys.tcp_endpoints**提供要授予和撤消连接权限的对象。 显示的有关端口和 IP 地址的信息不用于配置协议，并可能与实际的协议配置不匹配。 若要查看和配置协议，请使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**< 继承的列 >**||继承中的列[sys.endpoints](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)。|  
|**port**|int|端点正在侦听的端口号。 不可为 null。|  
|**is_dynamic_port**|bit|1 = 动态分配端口号。<br /><br /> 不可为 null。|  
|**ip 地址**|**nvarchar(45)**|LISTENER_IP 子句指定的侦听器 IP 地址。 可以为 Null。|  
  
## <a name="remarks"></a>注释  
 执行以下查询来收集有关端点和连接的信息。 没有当前连接或 TCP 连接的端点将显示为 NULL 值。 添加**其中**子句`WHERE des.session_id = @@SPID`返回有关当前连接的信息。  
  
```  
SELECT des.login_name, des.host_name, program_name,  dec.net_transport, des.login_time,   
e.name AS endpoint_name, e.protocol_desc, e.state_desc, e.is_admin_endpoint,   
t.port, t.is_dynamic_port, dec.local_net_address, dec.local_tcp_port   
FROM sys.endpoints AS e  
LEFT JOIN sys.tcp_endpoints AS t  
   ON e.endpoint_id = t.endpoint_id  
LEFT JOIN sys.dm_exec_sessions AS des  
   ON e.endpoint_id = des.endpoint_id  
LEFT JOIN sys.dm_exec_connections AS dec  
   ON des.session_id = dec.session_id;  
```  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [终结点目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
