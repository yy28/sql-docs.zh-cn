---
title: 将更改的跟踪标志行为 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- trace flags [SQL Server], behavior changes
ms.assetid: d739df96-2659-4383-8e10-194657632526
caps.latest.revision: 25
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f03a9db47c6296e7d1c4ab764488c44d343393c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36028943"
---
# <a name="changes-to-behavior-of-trace-flags"></a>对跟踪标志的行为的更改
  由某个会话设置的全局跟踪标志会立即在其他会话中生效。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中的一些跟踪标志在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中是不存在的。  
  
## <a name="component"></a>组件  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 建议在升级之前先禁用所有跟踪标志。 修改数据库可用性或恢复模式的跟踪标志可能会阻止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]成功升级的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 只有验证跟踪标志在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中是必需的并且仍有效之后，才能启用这些跟踪标志。 如果必须重新启用跟踪标志，应对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例执行更多测试。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 支持全局级别和会话级别的跟踪标志。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中，通过在 DBCC TRACEON 命令中使用其他参数 (-1)，可以将跟踪标志指定为局部的或全局的。 如果未指定此参数，则默认值为局部的。  
  
 此外，在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]，在会话 A 中设置跟踪标志不自动起已现有会话 B.中此跟踪标志相反，在任何跟踪标志设置在会话 B.中的第一个时间后才将生效此行为是不确定在[!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]和是确定在[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]及更高版本，其中立即在其他并发会话中设置在会话 A 中设置全局跟踪标志。  
  
## <a name="see-also"></a>请参阅  
 [数据库引擎升级问题](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 升级顾问&#91;新&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
