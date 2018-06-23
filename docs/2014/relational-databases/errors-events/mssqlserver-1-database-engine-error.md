---
title: MSSQLSERVER_-1 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "-1"
helpviewer_keywords:
- -1 (Database Engine error)
ms.assetid: bad25b91-eaed-46c0-a5b7-71117a32304c
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e8e439e4e20ab193685720b477f93573b41879fd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024585"
---
# <a name="mssqlserver-1"></a>MSSQLSERVER_-1
    
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
  
-   使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器工具使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能够通过 TCP 或 Named Pipes 协议接受远程连接。  
  
-   确保已配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器实例上的防火墙，为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 打开端口并打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 端口 (UDP 1434)。  
  
-   确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务已在服务器上启动。  
  
## <a name="see-also"></a>请参阅  
 [为数据库引擎访问配置 Windows 防火墙](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)   
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)   
 [网络协议和网络库](../../sql-server/install/network-protocols-and-network-libraries.md)   
 [客户端网络配置](../../database-engine/configure-windows/client-network-configuration.md)   
 [配置客户端协议](../../database-engine/configure-windows/configure-client-protocols.md)   
 [启用或禁用服务器网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
  