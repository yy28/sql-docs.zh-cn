---
title: "安装 SQL Server 复制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "组件 [SQL Server 复制]"
  - "命令行安装 [SQL Server 复制]"
  - "安装复制"
  - "复制 [SQL Server], 安装"
  - "命令提示符 [SQL Server 复制]"
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
caps.latest.revision: 41
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 41
---
# 安装 SQL Server 复制
  可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导或通过命令提示符安装复制组件。 请在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]或修改现有实例时安装复制组件。  
  
 安装复制组件后，必须配置服务器才可以使用复制。 有关详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的[配置分发](../../relational-databases/replication/configure-distribution.md)。  
  
> [!IMPORTANT]  
>  如果在修改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的现有实例时安装复制组件，则在安装完成后必须停止并重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。 此操作可帮助确保 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理能够识别复制代理子系统，并且可以在作业步骤中调用复制代理。  
  
## 使用安装程序安装复制  
 **在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   若要安装包括复制管理对象 (RMO) 在内的复制组件，请在安装向导的“功能选择”页上选择“SQL Server 复制”。  
  
## 从命令提示符安装复制  
 **在安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
-   请参阅[从命令提示符安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)。  
  
## 另请参阅  
 [安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)   
 [从命令提示符安装 SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [SQL Server 2016 各个版本支持的功能](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
  