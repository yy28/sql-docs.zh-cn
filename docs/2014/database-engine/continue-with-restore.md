---
title: 继续还原 |Microsoft Docs
description: 在 SQL Server 中，使用 "继续还原" 对话框指示是否要还原下一个备份集。
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.continuerestore.f1
ms.assetid: 987ac05f-57c0-49a9-9903-9889717aae4f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cd26a49b87615114b36c3fe57c7c6b50fbdbe7b0
ms.sourcegitcommit: 553d5b21bb4bf27e232b3af5cbdb80c3dcf24546
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/06/2020
ms.locfileid: "82849585"
---
# <a name="continue-with-restore"></a>继续还原
  使用 **“继续还原”** 对话框可指示是否要还原到下一个备份集。 若要延迟还原操作（例如，需要更换磁带），请待您做好继续操作的准备后再单击 **“确定”**。  
  
 单击 **“否”** 将终止还原顺序，但是会将数据库保持在还原状态。 若要在以后继续执行还原操作，请使用相应的 **“还原数据库”** 或 **“还原事务日志”** 任务。  
  
## <a name="options"></a>选项  
 **介质集**  
 显示下一个介质集名称（如果可用的话）。  
  
 **备份集**  
 显示备份集的名称。  
  
 **备份集说明**  
 显示备份集的说明。  
  
## <a name="see-also"></a>另请参阅  
 [查看备份磁带或文件的内容 (SQL Server)](../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)   
 [查看逻辑备份设备的属性和内容 (SQL Server)](../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)   
 [还原数据库备份 &#40;SQL Server Management Studio&#41;](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [还原事务日志备份 (SQL Server)](../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
  
