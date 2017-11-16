---
title: "回收 SQL Server 代理错误日志 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.ag.errorlog.recyclesqlagenterrorlogs.f1
ms.assetid: 10bc2dd1-0505-4527-8ec7-d3b4e5d6352b
caps.latest.revision: "3"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3404d3eceb9a57f9807ed2b47515fddb7331646a
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="recycle-sql-server-agent-error-logs"></a>回收 SQL Server 代理错误日志
使用此页可以回收 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理错误日志。 回收该日志将关闭当前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理错误日志并启动新的错误日志，而且不会重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理服务。 注意， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理保留九个最新的错误日志。 如果已经有九个错误日志，则回收错误日志会导致 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 代理删除最早的错误日志。  
  
## <a name="see-also"></a>另请参阅  
[SQL Server 代理错误日志](../../ssms/agent/sql-server-agent-error-log.md)  
  
