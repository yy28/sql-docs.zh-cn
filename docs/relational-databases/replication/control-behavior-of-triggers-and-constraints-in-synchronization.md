---
title: 同步中触发器和约束的控制行为 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
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
caps.latest.revision: 36
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9a4a6c79b7f7d719321ce731fd9b379719ca68ab
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37349219"
---
# <a name="control-behavior-of-triggers-and-constraints-in-synchronization"></a>同步中触发器和约束的控制行为
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  在同步期间，复制代理对复制表执行 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)、[UPDATE &#40;Transact-SQL&#41;](../../t-sql/queries/update-transact-sql.md) 和 [DELETE &#40;Transact-SQL&#41;](../../t-sql/statements/delete-transact-sql.md) 语句，这可能导致执行这些表上的数据操作语言 (DML) 触发器。 有些情况下，可能需要在同步期间防止这些触发器触发或防止约束被强制执行。 此行为取决于触发器或约束的创建方式。  
  
### <a name="to-prevent-triggers-from-executing-during-synchronization"></a>防止触发器在同步期间执行  
  
1.  创建新触发器时，请指定 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md) 的 NOT FOR REPLICATION 选项。  
  
2.  对于现有触发器，请指定 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md) 的 NOT FOR REPLICATION 选项。  
  
### <a name="to-prevent-constraints-from-being-enforced-during-synchronization"></a>防止约束在同步期间被强制执行  
  
1.  创建新 CHECK 或 FOREIGN KEY 约束时，请在 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md) 的约束定义中指定 CHECK NOT FOR REPLICATION 选项。  
  
## <a name="see-also"></a>另请参阅  
 [创建表（数据库引擎）](../../relational-databases/tables/create-tables-database-engine.md)  
  
  
