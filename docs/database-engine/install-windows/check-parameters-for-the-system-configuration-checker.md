---
title: "系统配置检查器的检查参数 | Microsoft Docs"
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
  - "安装 SQL Server, 系统配置检查"
  - "失败的系统配置检查 [SQL Server]"
  - "安装前验证配置"
  - "SCC [SQL Server]"
  - "系统配置检查器"
  - "安装前扫描计算机 [SQL Server]"
  - "安装前检查配置"
  - "状态信息 [SQL Server], 系统配置检查器"
  - "参数 [SQL Server], 系统配置检查器"
  - "配置检查器 [SQL Server]"
  - "安装程序 [SQL Server], 系统配置检查器"
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
caps.latest.revision: 46
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 46
---
# 系统配置检查器的检查参数
  在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中，系统配置检查器 (SCC) 会对将要安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机进行扫描。 SCC 将检查会使安装无法成功 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的情况。 在安装程序启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导之前，SCC 会检索每个项的状态。 然后，将检索结果与所需条件进行比较并提供如何排除妨碍性问题的指导。  
  
 系统配置检查器将会生成一个报告，该报告包含有关每个执行规则的简短说明以及执行状态。 该系统配置检查报告位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\。  
  
## 另请参阅  
 [安装 SQL Server 2016 的硬件和软件要求](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [安装 SQL Server 的安全注意事项](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [支持的版本升级](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
  