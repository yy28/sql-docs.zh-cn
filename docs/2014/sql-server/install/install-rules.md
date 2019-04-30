---
title: 安装规则 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SCC
- System Configuration Check, Setup
helpviewer_keywords:
- System Configuration Check page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, System Configuration Check page
- SCC [SQL Server]
ms.assetid: 168c0445-5651-42fc-91f4-d9f27d9e2281
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6105444259697caa655145c40f795469a9b6304f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63223139"
---
# <a name="install-rules"></a>安装规则
  在安装操作完成之前，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会验证您的计算机配置。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中，系统配置检查器 (SCC) 会对将要安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机进行扫描。 SCC 将检查阻止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装操作成功完成的条件。 在安装程序启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装向导之前，SCC 会检索每个项的状态。 然后，将检索结果与所需条件进行比较并提供如何排除妨碍性问题的指导。  
  
 系统配置检查将会生成一个报告，该报告包含有关每个执行规则的简短说明以及执行状态。 系统配置检查报告位于 %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\120\Setup Bootstrap\Log\\< YYYYMMDD_HHMM >\\。  
  
 在执行安装操作之前，请查看以下主题：  
  
1.  [安装 SQL Server 2014 的硬件和软件要求](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [SQL Server 2014 各个版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [安装 SQL Server 的安全注意事项](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [SQL Server 中的本地语言版本](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 其他参考：  
  
1.  [支持的版本和版本升级](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [安装故障转移群集前的准备工作](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="additional-rule-topics"></a>其他规则主题  
 有关方案特定的安装规则，请参阅以下主题：  
  
-   [安装规则](../../../2014/sql-server/install/installation-rules.md)  
  
-   [功能规则&#40;升级&#41;](../../../2014/sql-server/install/feature-rules-upgrade.md)  
  
-   [版本升级规则](../../../2014/sql-server/install/edition-upgrade-rules.md)  
  
-   [卸载规则](../../../2014/sql-server/install/uninstallation-rules.md)  
  
-   [准备映像规则](../../../2014/sql-server/install/prepare-image-rules.md)  
  
-   [完成映像规则](../../../2014/sql-server/install/complete-image-rules.md)  
  
  
