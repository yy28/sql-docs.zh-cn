---
title: 在网络上或不在网络上运行 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- verifying Server service has been started
- net start [SQL Server]
- command prompt [SQL Server], connections
- SQL Server services, networks
- status information [SQL Server], Server service
- running SQL Server
- networking [SQL Server], SQL Server with or without
- services [SQL Server], networks
- starting Server service
- SQL Server, running
ms.assetid: 54eac961-5c7a-4481-982d-f93a64b5c2f4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: db02b300e0f327a9186fb9b9af612d8f3f1ec452
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "67915993"
---
# <a name="run-sql-server-with-or-without-a-network"></a>在网络上或不在网络上运行 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 可以在网络上运行，也可以不在网络上运行。  
  
## <a name="running-sql-server-on-a-network"></a>在网络上运行 SQL Server  
 若要使 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 能够通过网络进行通信， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务必须正在运行。 默认情况下， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 将自动启动内置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 若要了解 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务是否已启动，请在命令提示符下键入：  
  
 **net start**  
  
 如果与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 关联的服务已经启动，那么 **net start** 输出中会显示下列服务：  
  
-   Analysis Services (MSSQLSERVER)  
  
-   SQL Server (MSSQLSERVER)  
  
-   SQL Server 代理 (MSSQLSERVER)  
  
## <a name="running-sql-server-without-a-network"></a>不在网络上运行 SQL Server  
 当不在网络上运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，无需启动内置的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务。 即使没有网络， [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、SQL Server 配置管理器、 **net start** 和 **net stop** 命令仍然有效。因此，无论是网络操作还是独立操作，启动和停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的过程是完全相同的。  
  
 当从本地客户端（如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlcmd **）连接到独立的**实例时，将不使用网络而使用本地管道直接连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 本地管道和网络管道的区别在于是否使用网络。 除非特别指明，否则本地管道和网络管道都使用标准管道 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .\pipe\sql\query) 与\\\\实例建立连接。  
  
 如果在连接到本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时不指定服务器名称，则使用的就是本地管道。 如果连接到本地 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例并显式指定了服务器名称，则所使用的就是网络管道或另一种网络进程间通信 (IPC) 机制，例如，网间数据包交换/有序数据包交换 (IPX/SPX)（假定已将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置成使用多种网络）。 由于独立的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不支持网络管道，因此必须在从客户端连接到  **实例时，省略不必要的 /**  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<Server_name> 自变量。 例如，若要从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] osql **连接到独立的**实例，请键入：  
  
 osql /Usa /P **saPassword>** _\<_  
  
  
