---
title: "将 AUTO_SHRINK 数据库选项设置为 OFF | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "最佳实践 [数据库引擎]"
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 将 AUTO_SHRINK 数据库选项设置为 OFF
  此规则检查 AUTO_SHRINK 数据库选项是否已设置为 OFF。 频繁收缩和展开数据库可能会导致物理碎片。  
  
## 最佳做法建议  
 将 AUTO_SHRINK 数据库选项设置为 OFF。 如果您知道以后将不再需要要回收的空间，则可以通过手动收缩数据库来回收该空间。  
  
## 有关详细信息  
 Microsoft 知识库文章 [315512](http://go.microsoft.com/fwlink/?linkid=117750)  
  
## 另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  