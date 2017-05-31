---
title: "检查包含可疑页的数据库的完整性 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 3b1ec9fe-f6c5-46f7-aa63-6e671be1572d
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b1fe88affe72749489540fe9e814e5549b197a79
ms.contentlocale: zh-cn
ms.lasthandoff: 04/11/2017

---
# <a name="check-integrity-of-database-with-suspect-pages"></a>检查包含可疑页的数据库的完整性
  此规则检查数据库状态设置为可疑的用户数据库。 当 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 读取包含 824 错误的数据库页时，该页将被视为可疑，其页 ID 将记录在 msdb 的 suspect_pages 表中，并且包含该页的数据库将设置为可疑。  
  
 错误 824 表示在读取操作期间检测到逻辑一致性错误。 此错误通常表示由有问题的 I/O 子系统组件引起的数据损坏。 这是一个威胁数据库完整性的严重错误条件，必须立即纠正。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
  
-   查看 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志以了解此数据库的 824 错误的详细信息。  
  
-   完成完整的数据库一致性检查 ([DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md))。  
  
-   实现在 [MSSQLSERVER_824](http://go.microsoft.com/fwlink/?LinkId=81397)中定义的用户操作。  
  
## <a name="for-more-information"></a>有关详细信息  
 [管理 suspect_pages 表 (SQL Server)](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
