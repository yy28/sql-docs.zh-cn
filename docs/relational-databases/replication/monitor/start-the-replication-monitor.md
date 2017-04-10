---
title: "启动复制监视器 | Microsoft Docs"
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
  - "复制监视器, 启动。"
ms.assetid: e037bd27-cc87-4ee9-9e5f-83f6d717cfa4
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# 启动复制监视器
  可以从任何 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 实例上的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]中启动复制监视器，也可以在命令提示符下启动复制监视器。 启动复制监视器后，将发布服务器添加至监视器。 有关详细信息，请参阅 [添加和从复制监视器删除发布服务器](../../../relational-databases/replication/monitor/add-and-remove-publishers-from-replication-monitor.md)。  
  
### 从 SQL Server Management Studio 启动复制监视器  
  
1.  连接至 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中的 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]实例，然后展开服务器节点。  
  
2.  用鼠标右键单击 **复制** 文件夹或其任何子文件夹，然后单击 **启动复制监视器**。  
  
### 从命令提示符启动复制监视器  
  
1.  在命令提示符下，导航到工具安装目录。 默认路径为 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]Tools\Binn\。  
  
2.  运行 sqlmonitor.exe。  
  
## 另请参阅  
 [监视复制](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  