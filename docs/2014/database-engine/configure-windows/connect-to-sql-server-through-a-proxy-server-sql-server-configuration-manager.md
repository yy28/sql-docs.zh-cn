---
title: 连接到 SQL Server 通过代理服务器 （SQL Server 配置管理器） |Microsoft 文档
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
caps.latest.revision: 20
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 1eb07c9e7b17caa4498ab8ddbc70388ae8a8cebc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138267"
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>通过代理服务器连接到 SQL Server（SQL Server 配置管理器）
  本主题介绍如何使用 SQL Server 配置管理器在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中通过代理服务器连接到 SQL Server。 若要通过远程 WinSock (RWS) 进行远程侦听，请定义代理服务器的本地地址表 (LAT)，以使侦听节点地址不在 LAT 条目范围内。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>通过 Microsoft 代理服务器连接到 SQL Server  
  
1.  请按照[配置服务器以侦听特定 TCP 端口（SQL Server 配置管理器）](configure-a-server-to-listen-on-a-specific-tcp-port.md)中的步骤，确定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用的 TCP/IP 端口，或将 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置为使用所需的端口。  
  
2.  在代理服务器中定义代理服务器的本地地址表 (LAT)，以使侦听节点地址不在 LAT 条目范围内。 有关详细信息，请参阅代理服务器文档。  
  
  