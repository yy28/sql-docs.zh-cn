---
title: "将 AUTO_CLOSE 数据库选项设置为 OFF | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "最佳实践 [数据库引擎]"
ms.assetid: e6b03364-263a-4ec4-9794-de9869d396ce
caps.latest.revision: 10
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 10
---
# 将 AUTO_CLOSE 数据库选项设置为 OFF
  此规则检查 AUTO_ CLOSE 选项是否设置为 OFF。 AUTO_CLOSE 设置为 ON 时，该选项可能导致频繁访问数据库而使性能下降，这是因为在每次连接后打开和关闭数据库增加了开销。 AUTO_CLOSE 还会在每次连接后刷新过程缓存。  
  
## 最佳做法建议  
 如果频繁访问数据库，则将数据库的 AUTO_CLOSE 选项设置为 OFF。  
  
## 有关详细信息  
 [ALTER DATABASE SET 选项 (Transact-SQL)](../Topic/ALTER%20DATABASE%20SET%20Options%20\(Transact-SQL\).md)  
  
## 另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  