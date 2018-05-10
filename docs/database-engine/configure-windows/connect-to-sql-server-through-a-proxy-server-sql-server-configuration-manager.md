---
title: 通过代理服务器连接到 SQL Server - SQL Server 配置管理器 | Microsoft Docs
ms.custom: ''
ms.date: 12/15/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ea68a2c59658f6edf44cd6d0d3edfccfd9d0bb82
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>通过代理服务器连接到 SQL Server（SQL Server 配置管理器）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  本主题介绍如何使用 SQL Server 配置管理器在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中通过代理服务器连接到 SQL Server。 若要通过远程 WinSock (RWS) 进行远程侦听，请定义代理服务器的本地地址表 (LAT)，以使侦听节点地址不在 LAT 条目范围内。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server 配置管理器  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>通过 Microsoft 代理服务器连接到 SQL Server  
  
1.  请按照[配置服务器以侦听特定 TCP 端口（SQL Server 配置管理器）](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)中的步骤，确定 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用的 TCP/IP 端口，或将 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 配置为使用所需的端口。  
  
2.  在代理服务器中定义代理服务器的本地地址表 (LAT)，以使侦听节点地址不在 LAT 条目范围内。 有关详细信息，请参阅代理服务器文档。  
  
>  [!NOTE]
>  本主题适用于本地 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 有关与 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]相关的连接问题，请参阅 [Troubleshoot connection issues to Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-troubleshoot-common-connection-issues)（排查 Azure SQL 数据库的连接问题）。  


