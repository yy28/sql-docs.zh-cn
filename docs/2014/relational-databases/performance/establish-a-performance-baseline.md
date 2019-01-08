---
title: 建立性能基线 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4b382545e9f7e5af1607d67539f2ae9f29cfdce3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52774549"
---
# <a name="establish-a-performance-baseline"></a>建立性能基线
  若要确定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 系统是否以最佳状态执行，可以定期进行性能度量（即使没有发生问题）以建立一条服务器性能基线。 将每组新的度量值与以前取得的度量值进行比较。  
  
 下列方面会影响 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的性能：  
  
-   系统资源（硬件）  
  
-   网络体系结构  
  
-   操作系统  
  
-   数据库应用程序  
  
-   客户端应用程序  
  
 至少，使用基线度量值确定：  
  
-   操作的峰值时间和非峰值时间。  
  
-   生产查询或批处理命令响应时间。  
  
-   数据库备份和还原所需时间。  
  
 建立服务器性能基线后，将基线统计与当前服务器性能进行比较。 对远高于或远低于基线的数字需要做进一步调查。 它们可能表明有需要调整或重新配置的区域。 例如，如果执行一组查询的时间增加，检查这些查询以确定能否重新编写它们，或者是否必须添加列统计信息或新索引。  
  
## <a name="see-also"></a>请参阅  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
