---
title: 查看数据库快照 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- database snapshots [SQL Server], viewing
- displaying database snapshots
- viewing database snapshots
ms.assetid: 123f19b2-0850-4033-8507-59ebdfb368ee
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0f3245deeed8983453a19276a137a2fbc9ed3882
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47785537"
---
# <a name="view-a-database-snapshot-sql-server"></a>查看数据库快照 (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
  
3.  若要列出 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例的数据库快照，对于非 NULL 值请查询 **sys.databases** 目录视图的 [source_database_id](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 列。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建数据库快照 (Transact-SQL)](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [将数据库恢复到数据库快照](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
-   [删除数据库快照 (Transact-SQL)](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
