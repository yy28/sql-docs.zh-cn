---
title: 修改使用 Banyan VINES 顺序包协议 (SPP)、 多协议、 AppleTalk 或 NWLink IPX SPX 网络协议的连接 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- network protocols [SQL Server], modifying connections
- SPP [SQL Server]
- NWLink IPX/SPX [SQL Server]
- connections [SQL Server]
- AppleTalk [SQL Server]
- Sequenced Packet Protocol [SQL Server]
- Multiprotocol Net-Library [SQL Server]
- Banyan VINES Sequenced Package Protocol [SQL Server]
- IPX/SPX [SQL Server]
- protocols [SQL Server], modifying connections
- RPC [SQL Server]
ms.assetid: 5c5ae453-cc5b-4898-95c7-ad34157b1f60
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0167af6c11abb12e8aa38a52a77707b81aecbe78
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018803"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>修改使用 Banyan VINES 顺序包协议 (SPP)、 多协议、 AppleTalk 或 NWLink IPX SPX 网络协议的连接
  升级顾问已检测到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支持的客户端服务器连接协议。 使用 Banyan VINES 顺序包协议 (SPP)、多协议 (RPC)、AppleTalk 或 NWLink IPX/SPX 网络协议的客户端应用程序必须通过支持的协议进行连接。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 不支持 Banyan VINES 顺序包协议 (SPP)、多协议、AppleTalk 或 NWLink IPX/SPX 网络协议。 以前使用这些协议连接的客户端必须选择其他协议。  
  
## <a name="corrective-action"></a>纠正措施  
 连接到服务器时，请将客户端应用程序更改为使用支持的协议。 如果设置的别名使用了不支持的协议，则必须修改该别名，使其使用支持的协议。  
  
 如果你的应用程序连接字符串中专门使用或其中一种协议的负载，由任一指定的网络 = DBMSRPCN rpc，网络 Appletalk 或网络 = DBMSADSN = DBMSVINN Banyan VINES 属性，或通过使用显式的前缀，如"spx:*服务器 \ 实例*"对于 SPX，"bv:*服务器*"为 Banyan VINES，"adsp:*服务器*"为 AppleTalk 或"rpc:*服务器*"为多协议，则您必须修改你的应用程序使用其中一个支持的协议。  
  
 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“选择网络协议”。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
