---
title: 控制同步期间触发器和约束的行为（复制 Transact-sql 编程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- identities [SQL Server replication]
- constraints [SQL Server], replication
- triggers [SQL Server], replication
- triggers [SQL Server replication]
- constraints [SQL Server replication]
- NOT FOR REPLICATION option
- NFR option
ms.assetid: 7c4e0f0e-cadc-4c99-98f4-69799b9b356b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 26d9a2431b91c1dc081345a06e7fe5a7533cbaa2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62721517"
---
# <a name="control-the-behavior-of-triggers-and-constraints-during-synchronization-replication-transact-sql-programming"></a>控制同步期间触发器和约束的行为（复制 Transact-SQL 编程）
  在同步期间，复制代理对复制表执行 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)、[UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) 和 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) 语句，这可能导致执行这些表上的数据操作语言 (DML) 触发器。 有些情况下，可能需要在同步期间防止这些触发器触发或防止约束被强制执行。 此行为取决于触发器或约束的创建方式。  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>防止触发器在同步期间执行  
  
1.  创建新触发器时，请指定 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql) 的 NOT FOR REPLICATION 选项。  
  
2.  对于现有触发器，请指定 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql) 的 NOT FOR REPLICATION 选项。  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>防止约束在同步期间被强制执行  
  
1.  创建新 CHECK 或 FOREIGN KEY 约束时，请在 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql) 的约束定义中指定 CHECK NOT FOR REPLICATION 选项。  
  
## <a name="see-also"></a>另请参阅  
 [创建表（数据库引擎）](../tables/create-tables-database-engine.md)  
  
  
