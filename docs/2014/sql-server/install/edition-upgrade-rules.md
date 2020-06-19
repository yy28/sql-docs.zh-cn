---
title: 版本升级规则 |Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 77c4d751-4fea-4e69-a7c8-ab8fc0dbadb2
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: fa8ba3986b4a7d6c0c7c03fb9bb1220a1c9280ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054811"
---
# <a name="edition-upgrade-rules"></a>版本升级规则
  在安装操作完成之前，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装程序会验证您的计算机配置。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装过程中，系统配置检查器 (SCC) 会对将要安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机进行扫描。 SCC 将检查阻止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 安装操作成功完成的条件。 在安装程序启动版本升级之前，SCC 会检索每个项的状态。 然后，将检索结果与所需条件进行比较并提供如何排除妨碍性问题的指导。  
  
 系统配置检查将会生成一个报告，该报告包含有关每个执行规则的简短说明以及执行状态。 系统配置检查报告位于% programfiles% \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \120\Setup Bootstrap\Log \\<YYYYMMDD_HHMM>\\ 。  
  
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
  
  
