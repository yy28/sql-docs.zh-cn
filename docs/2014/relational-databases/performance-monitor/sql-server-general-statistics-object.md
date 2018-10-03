---
title: SQL Server - General Statistics 对象 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:General Statistics
- General Statistics object
ms.assetid: c738e549-d7e7-4211-9ec3-064ac140af7c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: db96a90e9621949c528ea707be08beb5002177fe
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48067857"
---
# <a name="sql-server-general-statistics-object"></a>SQL Server General Statistics 对象
  **中的** SQLServer:General Statistics [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对象提供计数器，用于监视服务器范围内的常规活动，例如，当前的连接数和每秒与运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的计算机连接和断开的用户数。 这在大型联机事务处理 (OLTP) 类型系统（这种系统中有很多客户端与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例连接和断开连接）上工作时会非常有用。  
  
 下表介绍了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **General Statistics** 计数器。  
  
|SQL Server General Statistics 计数器|Description|  
|--------------------------------------------|-----------------|  
|**Active Temp Tables**|正在使用的临时表/表变量的数目。|  
|**Connection resets/sec**|从连接池启动的登录总次数。|  
|**Event Notifications Delayed Drop**|等待被某个系统线程删除的事件通知数。|  
|**HTTP Authenticated Requests**|每秒启动的验证过的 HTTP 请求数。|  
|**Logical Connections**|与系统建立的逻辑连接数。<br /><br /> 逻辑连接数的主要用途是支持多个活动结果集 (MARS) 请求。 对于 MARS 请求，每次应用程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进行连接时，都可能有多个与一个物理连接相对应的逻辑连接。<br /><br /> 在未使用 MARS 时，物理连接和逻辑连接之间的比率是 1:1。 因此，每次应用程序与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进行连接时，逻辑连接都将以 1 为增量增加。|  
|**Logins/sec**|每秒启动的登录总数。 这不包括已入池连接。|  
|**Logouts/sec**|每秒启动的注销操作总数。|  
|**Mars Deadlocks**|检测到的 MARS 死锁数。|  
|**Non-atomic yield rate**|每秒的非原子生成数。|  
|**Processes blocked**|当前阻塞的进程数。|  
|**SOAP Empty Requests**|每秒启动的空 SOAP 请求数。|  
|**SOAP Method Invocations**|每秒启动的 SOAP 方法调用数。|  
|**SOAP Session Initiate Requests**|每秒启动的 SOAP 会话启动请求数。|  
|**SOAP Session Terminate Requests**|每秒启动的 SOAP 会话终止请求数。|  
|**SOAP SQL Requests**|每秒启动的 SOAP SQL 请求数。|  
|**SOAP WSDL Requests**|每秒启动的 SOAP Web 服务描述语言请求数。|  
|**Temp Tables Creation Rate**|每秒创建的临时表/表变量的数目。|  
|**Temp Tables For Destruction**|等待被清除系统线程破坏的临时表/表变量数。|  
|**Trace Event Notifications Queue**|在内部队列中等待通过 Service Broker 发送的跟踪事件通知实例数。|  
|**事务**|事务登记（本地、DTC 和绑定的事务）的数目。|  
|**用户连接**|当前与 SQL Server 连接的用户数。|  
  
## <a name="see-also"></a>请参阅  
 [监视资源使用情况（系统监视器）](monitor-resource-usage-system-monitor.md)  
  
  
