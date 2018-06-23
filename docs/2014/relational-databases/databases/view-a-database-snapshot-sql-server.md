---
title: 查看数据库快照 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
caps.latest.revision: 21
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 201a96fd5fc47ae01177ef1d5685c2865f358880
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36130143"
---
# <a name="view-a-database-snapshot-sql-server"></a>查看数据库快照 (SQL Server)
  本主题说明如何使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 查看 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]数据库快照。  
  
> [!NOTE]  
>  若要创建、恢复到或删除数据库快照，必须使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]。  
  
 **本主题内容**  
  
-   **查看数据库快照，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 **查看数据库快照**  
  
1.  在对象资源管理器中，连接到 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 实例，然后展开该实例。  
  
2.  展开 **“数据库”**。  
  
3.  展开 **“数据库快照”**，然后选择要查看的快照。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **查看数据库快照**  
  
1.  连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]。  
  
2.  在标准菜单栏上，单击 **“新建查询”**。  
  
3.  若要列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的数据库快照，对于非 NULL 值请查询 **sys.databases** 目录视图的 [source_database_id](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 列。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建数据库快照 (Transact-SQL)](create-a-database-snapshot-transact-sql.md)  
  
-   [将数据库恢复到数据库快照](revert-a-database-to-a-database-snapshot.md)  
  
-   [删除数据库快照 (Transact-SQL)](drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>请参阅  
 [数据库快照 (SQL Server)](database-snapshots-sql-server.md)  
  
  
