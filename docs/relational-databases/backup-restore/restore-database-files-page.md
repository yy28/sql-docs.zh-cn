---
title: "还原数据库（“文件”页）| Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.restoredb.files.f1
- sql13.swb.restoredb.files.f1 in the code
ms.assetid: 714c36ea-a9f9-43a4-99f9-a6f73d1baf8e
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 43c7026aa357587fea7d4a9611b88237ed7896fd
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="restore-database-files-page"></a>还原数据库（“文件”页）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 使用“还原数据库”对话框的“文件”页以管理数据库中已选择要还原的特定文件。  
  
## <a name="options"></a>选项  
  
### <a name="restore-database-files-as"></a>将数据库文件还原为  
 用来向还原的文件分配新文件路径并进行管理。  
  
 **将所有文件重新定位到文件夹**  
 重新定位还原的文件。  
  
|选项|说明|  
|------------|-----------------|  
|**数据文件的文件夹**|输入或搜索应将还原的数据文件重新定位到的数据文件的文件夹名称。|  
|**日志文件的文件夹**|输入或搜索应将还原的日志文件文件重新定位到的日志文件的文件夹。|  
  
 **逻辑文件名**  
 对于每个要还原的数据库文件显示一行。  
  
 **文件类型**  
 显示文件类型。  
  
 **原始文件名**  
 显示已还原文件的原始文件路径。  
  
 **还原为**  
 列出用于另存还原文件的文件名。 输入或搜索适当的文件名。  
  
## <a name="see-also"></a>另请参阅  
 [还原数据库（“常规”页）](../../relational-databases/backup-restore/restore-database-general-page.md)   
 [还原数据库（“选项”页）](../../relational-databases/backup-restore/restore-database-options-page.md)   
 [RESTORE 参数 (Transact-SQL)](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [为磁带驱动器定义逻辑备份设备 (SQL Server)](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE (Transact-SQL)](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
