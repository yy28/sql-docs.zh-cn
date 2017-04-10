---
title: "保留锁配置选项默认值 | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "最佳实践 [数据库引擎]"
ms.assetid: f214f05b-5f0b-4786-b2ad-b8b4b6e58d72
caps.latest.revision: 12
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 12
---
# 保留锁配置选项默认值
  此规则检查锁配置选项的值。 此选项确定可用锁的最大数量。 这将限制 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 用于锁的内存量。 默认设置 0 使[!INCLUDE[ssDE](../../includes/ssde-md.md)]可以根据不断变化的系统要求动态地分配和解除分配锁结构。  
  
 如果锁为非零值，则批处理作业将停止，如果该值超出指定值，将生成“超出锁值”错误消息。  
  
## 最佳做法建议  
 在下面的语句中使用 sp_configure 系统存储过程将锁值更改为默认设置：  
  
```  
EXEC sp_configure 'locks', 0;  
```  
  
## 有关详细信息  
 [配置 locks 服务器配置选项](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md)  
  
 [sys.dm_tran_locks (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)  
  
 [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)  
  
 [Microsoft 知识库文章 271509](http://go.microsoft.com/fwlink/?linkid=117788)  
  
## 另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  