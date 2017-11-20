---
title: "disallow results from triggers 服务器配置选项 | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: configure-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ffca61b6490783e1721b6d66a01549b343e0422a
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>disallow results from triggers 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  使用 **disallow results from triggers** 选项可控制是否让触发器返回结果集。 返回结果集的触发器可能会导致应用程序出现意外的行为，而这些行为并不符合它们的设计意图。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 我们建议将此值设置为 1。  
  
 当设置为 1 时， **disallow results from triggers** 选项将设置为打开。 该选项的默认值为 0（关闭）。 如果将该选项设置为 1 (打开)，则触发器进行的任何返回结果集的尝试都将失败，用户将接收到下列错误消息：  
  
 “消息 524，级别 16，状态 1，过程 \<Procedure Name>，第 \<> 行  
  
 “触发器返回了结果集且服务器选项 "disallow_results_from_triggers" 为 TRUE。”  
  
 **disallow results from triggers** 选项应用于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例级别，它将确定实例中所有现有的触发器的行为。  
  
 **disallow results from triggers** 选项是一个高级选项。 如果使用 **sp_configure** 系统存储过程来更改该设置，则只有在“显示高级选项”设置为 1 时才能更改“禁止从触发器返回结果”选项。 该设置将立即生效，无需重新启动服务器。  
  
## <a name="see-also"></a>另请参阅  
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  

