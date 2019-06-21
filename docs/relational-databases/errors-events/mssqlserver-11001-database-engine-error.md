---
title: MSSQLSERVER_11001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "12001"
helpviewer_keywords:
- 11001 (Database Engine error)
ms.assetid: 53d4d63a-61e3-441f-bfe9-9d44f7a05fd4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5468b81930e1fd54602b0b91f9147b7c3b09c109
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63048293"
---
# <a name="mssqlserver11001"></a>MSSQLSERVER_11001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|11001|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称||  
|消息正文|在建立与服务器的连接时出错。  在连接到 SQL Server 时，在默认的设置下 SQL Server 不允许远程连接可能会导致此失败。 （提供程序：TCP 提供程序，错误:0 - 无法识别主机。）（.Net SqlClient 数据提供程序）|  
  
## <a name="explanation"></a>解释  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 客户端无法连接到服务器。 发生此错误的原因可能是客户端无法解析服务器的名称或服务器的名称不正确。  
  
## <a name="user-action"></a>用户操作  
确保已输入正确的客户端服务器名称，并且可以解析客户端服务器的名称。 若要检查 TCP/IP 名称解析，可以使用 Windows 操作系统中的 **ping** 命令。  
  
## <a name="see-also"></a>另请参阅  
[网络协议和网络库](~/sql-server/install/network-protocols-and-network-libraries.md)  
[客户端网络配置](~/database-engine/configure-windows/client-network-configuration.md)  
[配置客户端协议](~/database-engine/configure-windows/configure-client-protocols.md)  
[启用或禁用服务器网络协议](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
