---
title: "CONNECTIONPROPERTY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a5b023530bce0269af96918b0d578c6ca54293d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

返回处理请求时使用的唯一连接的连接属性的相关信息。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>参数  
*属性*  
连接的属性。 *属性*可以是以下值之一。
  
|值|数据类型|Description|  
|---|---|---|
|net_transport|**nvarchar （40)**|返回该连接使用的物理传输协议。 不可为 null。<br /><br /> 返回值： **HTTP**，**命名管道**，**会话**，**共享内存**， **SSL**， **TCP**，和**VIA**。<br /><br /> 注意： 始终返回**会话**当连接有多个活动结果集 (MARS) 启用，并启用连接池。|  
|protocol_type|**nvarchar （40)**|返回负载的协议类型。 此参数当前可区分 TDS (TSQL) 和 SOAP。 可以为 Null。|  
|auth_scheme|**nvarchar （40)**|返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接的身份验证方案。 身份验证方案为 Windows 身份验证（NTLM、KERBEROS、DIGEST、BASIC、NEGOTIATE）或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证。 不可为 null。|  
|local_net_address|**varchar(48)**|返回作为该连接的目标的服务器的 IP 地址。 仅适用于使用 TCP 传输提供程序的连接。 可以为 Null。|  
|local_tcp_port|**int**|如果连接是使用 TCP 传输的连接，则返回作为该连接的目标的服务器 TCP 端口。 可以为 Null。|  
|client_net_address|**varchar(48)**|请求连接到该服务器的客户端的地址。 可以为 Null。|  
|physical_net_transport|**nvarchar （40)**|返回该连接使用的物理传输协议。 如果连接启用了多个活动结果集 (MARS)，则返回准确结果。|  
|\<其他任何字符串 >||如果输入无效，则返回 NULL。|  
  
## <a name="remarks"></a>注释  
**local_net_address**和**local_tcp_port**返回中的 NULL [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)]。
  
返回的值并显示有关中的相应列的选项相同[sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)动态管理视图。 例如：
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>另请参阅
[sys.dm_exec_sessions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  

