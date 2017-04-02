---
title: "保证通过 Internet 复制的安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "安全性 [SQL Server 复制], Internet"
  - "Internet [SQL Server 复制], 安全性"
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
caps.latest.revision: 28
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 28
---
# 保证通过 Internet 复制的安全
  Internet 上的复制非常灵活，对移动订阅方而言尤为如此，但必须适当地配置 Internet 复制以确保具有足够的安全性。 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 建议使用下列两种技术之一在 Internet 上安全地共享信息：  
  
-   虚拟专用网络 (VPN)  
  
-   合并复制的 Web 同步选项  
  
## 虚拟专用网络  
 虚拟专用网络为在 Internet 上复制 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据提供了简便安全的分层方法。 Internet 上的 VPN 连接逻辑上可以像站点间的广域网 (WAN) 链接一样使用。  
  
 这通过允许用户通过 Internet 或使用一种协议，如另一个公用网络的隧道 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 点对点隧道协议 (PPTP) 适用于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 4.0 或 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000 操作系统或第二层隧道协议 (L2TP) 可用于 Windows 2000 操作系统。 此过程提供类似于专用网络中的安全性和功能。  
  
 有关设置 VPN 的详细信息，请参阅 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 文档。  
  
## 通过 IIS 的 Web 同步  
 合并复制的 Web 同步选项提供了用 HTTPS 协议复制数据的功能，这是一种通过防火墙复制数据的简便方法。 有关详细信息，请参阅 [配置 Web 同步](../../../relational-databases/replication/configure-web-synchronization.md) 和 [Web 同步的安全体系结构](../../../relational-databases/replication/security/security-architecture-for-web-synchronization.md)。  
  
## 另请参阅  
 [复制安全最佳实践](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全和保护与 #40;复制和 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)  
  
  