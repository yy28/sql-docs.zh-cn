---
title: MSSQLSERVER_-1 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- "-1"
helpviewer_keywords:
- -1 (Database Engine error)
ms.assetid: bad25b91-eaed-46c0-a5b7-71117a32304c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 048db39c941cd54977c09450097724ebc7a2c584
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver-1"></a>MSSQLSERVER_-1
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|事件 ID|-1|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在建立与服务器的连接时出错。  在连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，在默认的设置下 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不允许进行远程连接可能会导致此失败。 (访问接口: SQL 网络接口，错误: 28 - 服务器不支持请求的协议) (Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，错误: -1)|  
  
## <a name="explanation"></a>解释  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端无法连接到服务器。 此错误可能由以下某个原因引起：  
  
-   指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称无效。  
  
-   TCP 或 Named Pipes 协议未启用。  
  
-   服务器上的防火墙拒绝了此连接。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务 (sqlbrowser) 未启动。  
  
## <a name="user-action"></a>用户操作  
若要解决此错误，请尝试执行下列操作之一：  
  
-   检查连接字符串中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名称的拼写。  
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器工具使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能够通过 TCP 或 Named Pipes 协议接受远程连接。 有关接受远程连接的详细信息，请参阅[启用或禁用服务器网络协议](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)。  
  
-   确保已配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器实例上的防火墙，为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 打开端口并打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 端口 (UDP 1434)。  
  
-   确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务已在服务器上启动。  
  
## <a name="see-also"></a>另请参阅  
[为数据库引擎访问配置 Windows 防火墙](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[配置客户端协议](~/database-engine/configure-windows/configure-client-protocols.md)  
[网络协议和网络库](~/sql-server/install/network-protocols-and-network-libraries.md)  
[客户端网络配置](~/database-engine/configure-windows/client-network-configuration.md)  
[配置客户端协议](~/database-engine/configure-windows/configure-client-protocols.md)  
[启用或禁用服务器网络协议](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
