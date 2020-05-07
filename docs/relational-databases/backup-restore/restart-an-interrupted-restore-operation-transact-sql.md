---
title: 重启中断的还原 (Transact-SQL)
description: 此示例演示如何使用 Transact-SQL 重新启动中断的还原操作。
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- interrupted restore operation
- restoring databases [SQL Server], restarting interrupted operation
- resetting options changed after backup
- database restores [SQL Server], restarting interrupted operation
- restarting interrupted restore operation
- restoring interrupted operation [SQL Server]
ms.assetid: 6413a07d-fd90-448d-8f29-12c5a1972618
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4eb0e80201694ca6bb6109cc4013500f31a8bf2a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180841"
---
# <a name="restart-an-interrupted-restore-operation-transact-sql"></a>重新启动中断的还原操作 (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  本主题说明如何重新启动中断的还原操作。  
  
### <a name="to-restart-an-interrupted-restore-operation"></a>重新启动中断的还原操作  
  
1.  再次执行中断的 RESTORE 语句，同时指定：  
  
    -   原 RESTORE 语句中使用的相同子句。  
  
    -   RESTART 子句。  
  
## <a name="example"></a>示例  
 以下示例将重新启动中断的还原操作。  
  
```sql  
-- Restore a full database backup of the AdventureWorks database.  
RESTORE DATABASE AdventureWorks  
   FROM DISK = 'C:\AdventureWorks.bck'  
GO  
-- The restore operation halted prematurely.  
-- Repeat the original RESTORE statement specifying WITH RESTART.  
RESTORE DATABASE AdventureWorks   
   FROM DISK = 'C:\AdventureWorks.bck'  
   WITH RESTART  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [完整数据库还原（完整恢复模式）](../../relational-databases/backup-restore/complete-database-restores-full-recovery-model.md)   
 [完整数据库还原（简单恢复模式）](../../relational-databases/backup-restore/complete-database-restores-simple-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
