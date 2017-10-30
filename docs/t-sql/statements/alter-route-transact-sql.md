---
title: "ALTER 路由 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROUTE_TSQL
- ALTER ROUTE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ROUTE statement
- dropping routes
- modifying routes
- removing routes
- routes [Service Broker], modifying
ms.assetid: 8dfb7b16-3dac-4e1e-8c97-adf2aad07830
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 39e39b8688e2350d27e664b4a1517584c11df941
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-route-transact-sql"></a>ALTER ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中现有路由的路由信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER ROUTE route_name  
WITH    
  [ SERVICE_NAME = 'service_name' [ , ] ]  
  [ BROKER_INSTANCE = 'broker_instance' [ , ] ]  
  [ LIFETIME = route_lifetime [ , ] ]  
  [ ADDRESS =  'next_hop_address' [ , ] ]  
  [ MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
  
```  
  
## <a name="arguments"></a>参数  
 *route_name*  
 要更改的路由的名称。 不能指定服务器、数据库和架构名称。  
  
 替换为  
 引入对要更改的路由进行定义的子句。  
  
 SERVICE_NAME **=***service_name*  
 指定此路由指向的远程服务的名称。 *Service_name*必须完全匹配的名称远程服务使用。 [!INCLUDE[ssSB](../../includes/sssb-md.md)]使用逐字节比较，以匹配*service_name*。 也就是说，这种比较区分大小写，并且不考虑当前的排序规则。 服务名称的路由**SQL/ServiceBroker/BrokerConfiguration**是到 Broker 配置通知服务的路由。 指向此服务的路由不能指定 Broker 实例。  
  
 如果省略 SERVICE_NAME 子句，则路由的服务名称保持不变。  
  
 BROKER_INSTANCE **=***broker_instance*  
 指定承载目标服务的数据库。 *Broker_instance*参数必须是远程数据库，可以通过在所选数据库中运行以下查询获取的 broker 实例标识符：  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 如果省略 BROKER_INSTANCE 子句，则路由的 Broker 实例保持不变。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 生存期 **=**  *route_lifetime*  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在路由表中保留路由的时间（秒）。 在生存期结束后，相应的路由即过期，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在为新会话选择路由时将不再考虑该路由。 如果省略此子句，则路由的生存期保持不变。  
  
 地址**=***next_hop_address 的*  
 指定此路由的网络地址。 *Next_hop_address*采用以下格式指定 TCP/IP 地址：  
  
 **TCP: / /** { *dns_name* | *netbios_name* |*ip_address* } **:** *port_number*  
  
 指定*port_number*必须与匹配的端口号[!INCLUDE[ssSB](../../includes/sssb-md.md)]实例的终结点[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在指定的计算机。 这可以通过在选定数据库中运行如下查询获得：  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 当路由指定了**'LOCAL'**为*next_hop_address*，消息传递到内的当前实例的服务[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 当路由指定了**'TRANSPORT'**为*next_hop_address*，基于该服务的名称的网络地址确定网络地址。 指定的路由**'TRANSPORT'**可以指定服务名称或代理实例。  
  
 当*next_hop_address*为主体服务器为数据库镜像，则还必须指定镜像服务器 MIRROR_ADDRESS。 否则，此路由将不能自动向镜像服务器进行故障转移。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
 MIRROR_ADDRESS **=***next_hop_mirror_address*  
 指定其主体服务器位于镜像对的镜像服务器的网络地址*next_hop_address*。 *Next_hop_mirror_address*采用以下格式指定 TCP/IP 地址：  
  
 **TCP: / /**{ *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 指定*port_number*必须与匹配的端口号[!INCLUDE[ssSB](../../includes/sssb-md.md)]实例的终结点[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在指定的计算机。 这可以通过在选定数据库中运行如下查询获得：  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 如果指定了 MIRROR_ADDRESS，则路由必须指定 SERVICE_NAME 子句和 BROKER_INSTANCE 子句。 指定的路由**'LOCAL'**或**'TRANSPORT'**为*next_hop_address*可能未指定的镜像地址。  
  
> [!NOTE]  
>  此选项在包含数据库中不可用。  
  
## <a name="remarks"></a>注释  
 存储的路由的路由表是可通过读取的元数据表**sys.routes**目录视图。 路由表只能通过 CREATE ROUTE、ALTER ROUTE 和 DROP ROUTE 语句进行更新。  
  
 未在 ALTER ROUTE 命令中指定的子句保持不变。 因此，无法通过对路由执行 ALTER 语句来指定此路由不超时、此路由与任何服务名称匹配或此路由与任何 Broker 实例匹配。 若要更改路由的这些特征，必须删除现有路由，然后使用新的信息创建一个新路由。  
  
 当路由指定了**'TRANSPORT'**为*next_hop_address*，基于服务的名称确定网络地址。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可成功处理对有效的格式中的网络地址以开头的服务名称*next_hop_address*。 名称包含有效网络地址的服务将路由到服务名称中的网络地址。  
  
 路由表可以包含任意数目的指定相同服务、网络地址和/或 Broker 实例标识符的路由。 在此情况下，[!INCLUDE[ssSB](../../includes/sssb-md.md)] 会使用专门的过程，在会话中指定的信息与路由表中的信息之间找出最匹配的项，以此来选择路由。  
  
 若要更改服务的 AUTHORIZATION，请使用 ALTER AUTHORIZATION 语句。  
  
## <a name="permissions"></a>Permissions  
 权限更改路由的默认路由的成员的所有者为**db_ddladmin**或**db_owner**固定数据库角色和成员的**sysadmin**固定服务器角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-the-service-for-a-route"></a>A. 更改路由的服务  
 以下示例将 `ExpenseRoute` 路由修改为指向远程服务 `//Adventure-Works.com/Expenses`。  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     SERVICE_NAME = '//Adventure-Works.com/Expenses';  
```  
  
### <a name="b-changing-the-target-database-for-a-route"></a>B. 更改路由的目标数据库  
 以下示例将 `ExpenseRoute` 路由的目标数据库更改为由唯一标识符 `D8D4D268-00A3-4C62-8F91-634B89B1E317.` 标识的数据库  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317';  
```  
  
### <a name="c-changing-the-address-for-a-route"></a>C. 更改路由的地址  
 以下示例将 `ExpenseRoute` 路由的网络地址更改为 IP 地址为 `1234` 的主机上的 TCP 端口 `10.2.19.72`。  
  
```  
ALTER ROUTE ExpenseRoute   
   WITH   
     ADDRESS = 'TCP://10.2.19.72:1234';  
```  
  
### <a name="d-changing-the-database-and-address-for-a-route"></a>D. 更改路由的数据库和地址  
 下例将 `ExpenseRoute` 路由的网络地址更改为 DNS 名称为 `1234` 的主机上的 TCP 端口 `www.Adventure-Works.com`。 它还将目标数据库更改为由唯一标识符 `D8D4D268-00A3-4C62-8F91-634B89B1E317` 标识的数据库。  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317',  
     ADDRESS = 'TCP://www.Adventure-Works.com:1234';  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE ROUTE (Transact SQL)](../../t-sql/statements/create-route-transact-sql.md)   
 [删除路由 &#40;Transact SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

