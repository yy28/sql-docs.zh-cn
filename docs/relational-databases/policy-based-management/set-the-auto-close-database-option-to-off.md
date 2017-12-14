---
title: "将 AUTO_CLOSE 数据库选项设置为 OFF | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
caps.latest.revision: "10"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: f7e0a92a62abd1239b9f0d45d37c68e490505826
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="set-the-autoclose-database-option-to-off"></a>将 AUTO_CLOSE 数据库选项设置为 OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]此规则检查 AUTO_ CLOSE 选项是否设置为 OFF。 AUTO_CLOSE 设置为 ON 时，该选项可能导致频繁访问数据库而使性能下降，这是因为在每次连接后打开和关闭数据库增加了开销。 AUTO_CLOSE 还会在每次连接后刷新过程缓存。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 如果频繁访问数据库，则将数据库的 AUTO_CLOSE 选项设置为 OFF。  
  
## <a name="for-more-information"></a>有关详细信息  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
