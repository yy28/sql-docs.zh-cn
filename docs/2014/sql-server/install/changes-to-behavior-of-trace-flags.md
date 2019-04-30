---
title: 跟踪标志行为的更改 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 421420089526540929bfc4ade32799634a823391
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63215638"
---
# <a name="changes-to-behavior-of-trace-flags"></a>对跟踪标志的行为的更改
  由某个会话设置的全局跟踪标志会立即在其他会话中生效。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中的一些跟踪标志在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中是不存在的。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>描述  
 建议在升级之前先禁用所有跟踪标志。 修改数据库可用性或恢复模式的跟踪标志可能会阻止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]无法成功升级的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 只有验证跟踪标志在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中是必需的并且仍有效之后，才能启用这些跟踪标志。 如果必须重新启用跟踪标志，应对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例执行更多测试。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持全局级别和会话级别的跟踪标志。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，通过在 DBCC TRACEON 命令中使用其他参数 (-1)，可以将跟踪标志指定为局部的或全局的。 如果未指定此参数，则默认值为局部的。  
  
 此外，在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，会话 A 中设置的跟踪标志将不会自动生效中已有的会话 b。相反，此跟踪标志之后才生效第一次会话 B.中设置任何跟踪标志此行为是在具有不确定性[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]和具有确定性[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更高版本，在其中立即在其他并发会话中设置全局跟踪标志在会话 A 中设置。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
