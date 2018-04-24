---
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95c95ad472c5b5d4cb5420fa3b0da8f88053c0c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回处理请求时使用的唯一连接的连接属性的相关信息。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>参数  
property  
连接的属性。 property 可以是下列值之一。
  
|ReplTest1|数据类型|Description|  
|---|---|---|
|net_transport|**nvarchar(40)**|返回该连接使用的物理传输协议。 不可为 null。<br /><br /> 返回值为：HTTP、命名管道、会话、共享内存、SSL、TCP 和 VIA。<br /><br /> 注意：如果连接启用了多个活动结果集 (MARS)，并且启用了连接池，则始终返回 Session。|  
|protocol_type|**nvarchar(40)**|返回负载的协议类型。 此参数当前可区分 TDS (TSQL) 和 SOAP。 可以为 Null。|  
|auth_scheme|**nvarchar(40)**|返回连接的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证方案。 身份验证方案为 Windows 身份验证（NTLM、KERBEROS、DIGEST、BASIC、NEGOTIATE）或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 不可为 null。|  
|local_net_address|**varchar(48)**|返回作为该连接的目标的服务器的 IP 地址。 仅适用于使用 TCP 传输提供程序的连接。 可以为 Null。|  
|local_tcp_port|**int**|如果连接是使用 TCP 传输的连接，则返回作为该连接的目标的服务器 TCP 端口。 可以为 Null。|  
|client_net_address|**varchar(48)**|请求连接到该服务器的客户端的地址。 可以为 Null。|  
|physical_net_transport|**nvarchar(40)**|返回该连接使用的物理传输协议。 如果连接启用了多个活动结果集 (MARS)，则返回准确结果。|  
|\<任何其他字符串>||如果输入无效，则返回 NULL。|  
  
## <a name="remarks"></a>Remarks  
local_net_address 和 local_tcp_port 在 [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] 中返回 NULL。
  
返回的值与为 [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md) 动态管理视图中的相应列显示的选项相同。 例如：
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>另请参阅
[sys.dm_exec_sessions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  
