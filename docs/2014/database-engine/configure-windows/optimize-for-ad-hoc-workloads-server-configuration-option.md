---
title: optimize for ad hoc workloads 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- optimize for ad hoc workloads option
ms.assetid: 0972e028-3a8e-454b-a186-e814a1d431f2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7edf279b49374823c9083005be9b8d047b003f62
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62781433"
---
# <a name="optimize-for-ad-hoc-workloads-server-configuration-option"></a>“针对即席工作负荷进行优化”服务器配置选项
  “针对即席工作负荷进行优化”  选项用于提高包含许多一次性临时批处理的工作负荷计划缓存的效率。 如果该选项设置为 1，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将在首次编译批处理时在计划缓存中存储一个编译的小计划存根，而不是存储完全编译的计划。 这种情况下不会让未重复使用的编译计划填充计划缓存，从而有助于缓解内存压力。  
  
 编译的计划存根使[!INCLUDE[ssDE](../../includes/ssde-md.md)]能够识别此临时批处理以前已经过编译，但只存储了编译计划存根，因此当再次调用（编译或执行）此批处理时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]会对此批处理进行编译，从计划缓存中删除编译计划存根并将完全编译的计划添加到计划缓存中。  
  
 将“针对即席工作负荷进行优化” **** 设置为 1 只会影响新计划；已在计划缓存中的计划不受影响。  
  
 编译计划存根是 sys.dm_exec_cached_plans 目录视图显示的 cacheobjtype 之一。 它具有唯一的 SQL 句柄和计划句柄。 编译计划存根没有与其关联的执行计划，并且查询计划句柄不会返回 XML 显示计划。  
  
 跟踪标志 8032 将缓存限制参数还原为 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] RTM 设置，此设置通常允许更大的缓存。 当频繁重复使用的缓存条目不适合缓存时，以及当 *“针对即席工作负荷进行优化”服务器配置选项* 未能解决与计划缓存相关的问题时，请使用此设置。  
  
> [!WARNING]  
>  如果大缓存使较少的内存可用于其他内存消耗者（如缓冲池），则跟踪标志 8032 可能导致性能较差。  
  
## <a name="see-also"></a>另请参阅  
 [sys. dm_exec_cached_plans &#40;Transact-sql&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-cached-plans-transact-sql)   
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
