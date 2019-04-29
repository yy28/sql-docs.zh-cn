---
title: 将数据库还原到标记的事务 (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.markedtransaction.f1
helpviewer_keywords:
- database restores [SQL Server], marked transactions
- restoring databases [SQL Server], marked transactions
- marked transactions [SQL Server], restoring
ms.assetid: 8f0ea144-1819-4832-905f-e5d0f49b066b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 919c10372e397f0c2d66d7648363aef7916ec598
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62875603"
---
# <a name="restore-a-database-to-a-marked-transaction-sql-server-management-studio"></a>将数据库还原到标记的事务 (SQL Server Management Studio)
  数据库处于还原状态时，可以使用 **“还原事务日志”** 对话框将数据库还原到可用日志备份中的标记的事务。  
  
> [!NOTE]  
>  有关详细信息，请参阅[使用标记事务一致恢复相关数据库（完全恢复模式）](use-marked-transactions-to-recover-related-databases-consistently.md)和[恢复包含标记事务的相关数据库](recovery-of-related-databases-that-contain-marked-transaction.md)。  
  
### <a name="to-restore-a-marked-transaction"></a>还原标记的事务  
  
1.  连接到相应的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例之后，在对象资源管理器中，单击服务器名称以展开服务器树。  
  
2.  展开 **“数据库”**，然后根据数据库的不同，选择用户数据库，或展开 **“系统数据库”** ，再选择系统数据库。  
  
3.  右键单击数据库，指向“任务”，再单击“还原”。  
  
4.  单击 **“事务日志”**，这将打开 **“还原事务日志”** 对话框。  
  
5.  在 **“常规”** 页上的 **“还原到”** 部分中，选择 **“标记的事务”**，将打开 **“选择标记的事务”** 对话框。 此对话框中将以网格列表的形式显示选择的事务日志备份中可用的标记的事务。  
  
     默认情况下，将一直还原到（但不包含）标记的事务为止。 若要同时还原标记的事务，请选择 **“包含标记的事务”**。  
  
     下表列出了网格的列标题并对列值进行了说明。  
  
    |Header|ReplTest1|  
    |------------|-----------|  
    |\<blank>|显示一个用于选择标记的复选框。|  
    |**事务标记**|提交事务时，用户为标记的事务指定的名称。|  
    |**Date**|事务的提交日期及时间。 事务日期和时间显示为 **msdbgmarkhistory** 表中所记录的日期和时间，而非客户端计算机的日期和时间。|  
    |**说明**|提交事务时，用户为标记的事务指定的说明（如果有的话）。|  
    |**LSN**|所标记事务的日志序列号。|  
    |**“数据库”**|提交标记的事务时所在数据库的名称。|  
    |**用户名**|提交标记事务的数据库用户的名称。|  
  
## <a name="see-also"></a>请参阅  
 [还原数据库备份&#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [还原事务日志备份 (SQL Server)](restore-a-transaction-log-backup-sql-server.md)  
  
  
