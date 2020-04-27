---
title: 功能规则（升级） |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 653b15db-a984-4b4b-b224-81b0285b099b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3399c6e8c73916e613197aec2ee0499098a8fa86
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095391"
---
# <a name="feature-rules-upgrade"></a>功能规则（升级）
  在安装操作完成之前，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会验证您的计算机配置。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装期间，系统会扫描将安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机，并检查是否有妨碍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 成功安装的任何情况。 在安装程序启动升级向导之前，系统会检索每一项的状态。 然后，将检索结果与所需条件进行比较并提供如何排除妨碍性问题的指导。  
  
 系统配置检查将会生成一个报告，该报告包含有关每个执行规则的简短说明以及执行状态。 系统配置检查报告位于%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]programfiles% \120\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>。 \\  
  
 在执行安装操作之前，请查看以下主题：  
  
1.  [安装 SQL Server 2014 的硬件和软件要求](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [SQL Server 2014 各个版本支持的功能](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [安装 SQL Server 的安全注意事项](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [SQL Server 中的本地语言版本](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 其他参考：  
  
1.  [支持的版本和版本升级](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [安装故障转移群集前的准备工作](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="see-also"></a>另请参阅  
 [安装规则](../../../2014/sql-server/install/install-rules.md)  
  
  
