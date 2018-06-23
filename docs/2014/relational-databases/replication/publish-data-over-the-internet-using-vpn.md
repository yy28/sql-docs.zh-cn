---
title: 使用 VPN 通过 Internet 发布数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VPNs [SQL Server replication]
- Web publishing [SQL Server replication], VPNs
- Internet [SQL Server replication], VPNs
ms.assetid: 9ffb6546-9973-4574-aaa0-8fe0017e3601
caps.latest.revision: 32
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8e8da7742a29f46e289c35c3e2fff7480f8e206b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125832"
---
# <a name="publish-data-over-the-internet-using-vpn"></a>使用 VPN 通过 Internet 发布数据
  通过使用虚拟专用网络 (VPN) 技术，用户可以在家中、分支机构、远程客户端和其他公司通过 Internet 连接到企业网络进行工作，同时保持通信安全。 用户可以像在局域网 (LAN) 上那样使用 Windows 身份验证。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 复制的所有类型都可以通过 VPN 复制数据，但如果使用的是合并复制，则应该考虑使用 Web 同步。因为 Web 同步不需要使用 VPN。 有关详细信息，请参阅 [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md)。  
  
 VPN 包含客户端软件，以便计算机可以通过 Internet（特殊情况下甚至可以是 Intranet）连接到专用计算机或服务器上的软件。 用户可以选择使用两端加密和用户身份验证的方法。 Internet 上的 VPN 连接逻辑上可以像站点间的广域网 (WAN) 链接一样使用。  
  
 VPN 通过一个网络连接另一个网络的组件。 为了连接，用户应以使用协议（例如 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 点对点隧道协议 [PPTP] 或第二层隧道协议 [L2TP]）的 Internet 或其他公用网络为隧道。 此过程提供了与以前仅在专用网络中实现的相同安全性和功能。 在 Microsoft Windows NT 4.0 版和 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000（和更高版本）的操作系统中可以使用 PPTP；在 Windows 2000 和更高版本的操作系统中可以使用 L2TP。  
  
 对于用户来说，Internet 的中间路由基础结构是不可见的，数据就好像通过专门的专用链接发送一样。 就用户而言，VPN 是用户计算机和公司服务器之间的点对点连接。  
  
 将远程客户端配置为使用 VPN 进行连接，而且客户端能够访问 Internet 并已登录到公司 LAN 之后，可以像远程客户端直接连接在 LAN 上一样配置复制。 出于安全考虑，通过 VPN 连接的用户和直接连接在 LAN 上的用户可能使用不同的网络资源。  
  
 有关设置 VPN 的详细信息，请参阅 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 文档。  
  
## <a name="see-also"></a>请参阅  
 [通过 Internet 复制](replication-over-the-internet.md)  
  
  