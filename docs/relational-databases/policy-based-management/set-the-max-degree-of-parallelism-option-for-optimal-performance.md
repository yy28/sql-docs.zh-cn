---
title: "设置最大并行度选项以获取最佳性能 | Microsoft Docs"
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
ms.assetid: ec908006-67ae-4674-9a61-25ea741d6197
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# 设置最大并行度选项以获取最佳性能
  此规则确定最大并行度 (MAXDOP) 选项是否设置为大于 8 的值。 将此选项设置为大于 8 的值通常导致不必要的资源消耗和性能下降。  
  
## 最佳做法建议  
 通过使用 sp_configure 将最大并行度选项设置为 8 或更小。  
  
## 有关详细信息  
 [Microsoft 知识库文章 329204](http://go.microsoft.com/fwlink/?linkid=117786)  
  
 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)  
  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  