---
title: 删除数据库快照 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- removing database snapshots
- deleting database snapshots
- database snapshots [SQL Server], deleting
ms.assetid: ad70ec97-d5fb-41aa-b72a-915e74b61b76
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0738c1e661c679022a6a635af756003fdd98dfe0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086017"
---
# <a name="drop-a-database-snapshot-transact-sql"></a>删除数据库快照 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  删除数据库快照将删除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的数据库快照，并删除快照使用的稀疏文件。 删除数据库快照会终止所有到此快照的用户连接。  
  
## <a name="security"></a>Security  
  
###  <a name="Permissions"></a> 权限  
 具有 DROP DATABASE 权限的任何用户都可以删除数据库快照。  
  
##  <a name="TsqlProcedure"></a> 如何删除数据库快照（使用 Transact-SQL）  
 **删除数据库快照**  
  
1.  标识要删除的数据库快照。 您可以在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中查看数据库快照。 有关详细信息，请参阅 [查看数据库快照 (SQL Server)](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)中查看数据库快照。  
  
2.  执行 [DROP DATABASE](../../t-sql/statements/drop-database-transact-sql.md) 语句，并指定要删除的数据库快照的名称。 语法如下：  
  
     DROP DATABASE *database_snapshot_name* [ **,** ...*n* ]  
  
     其中， *database_snapshot_name* 是要删除的数据库快照的名称。  
  
####  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例将删除名为 SalesSnapshot0600 的数据库快照，而不影响源数据库。  
  
```  
DROP DATABASE SalesSnapshot0600 ;  
```  
  
 到 SalesSnapshot0600 的所有用户连接都被终止，并删除快照使用的所有 NTFS 文件系统稀疏文件。  
  
> [!NOTE]  
>  有关数据库快照如何使用稀疏文件的信息，请参阅 [数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)中查看数据库快照。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [创建数据库快照 (Transact-SQL)](../../relational-databases/databases/create-a-database-snapshot-transact-sql.md)  
  
-   [查看数据库快照 (SQL Server)](../../relational-databases/databases/view-a-database-snapshot-sql-server.md)  
  
-   [将数据库恢复到数据库快照](../../relational-databases/databases/revert-a-database-to-a-database-snapshot.md)  
  
  
## <a name="see-also"></a>另请参阅  
 [DROP DATABASE (Transact SQL)](../../t-sql/statements/drop-database-transact-sql.md)   
 [数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  
