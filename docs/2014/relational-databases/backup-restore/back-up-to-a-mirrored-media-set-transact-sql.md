---
title: 备份到镜像媒体集 (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 5fc43a5d-dfd6-4c53-a4ef-3c8da23ccc81
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 88ea15fabe8e8fd6630d3430417879c7104dff67
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62876919"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>备份镜像媒体集 (Transact-SQL)
  本主题介绍在备份 [!INCLUDE[tsql](../../includes/tsql-md.md)][数据库时如何使用](/sql/t-sql/statements/backup-transact-sql) BACKUP [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 语句指定镜像介质集。 在 BACKUP 语句中的 TO 子句中指定第一个镜像。 然后，在它自己的 MIRROR TO 子句中指定每个镜像。 TO 和 MIRROR TO 子句必须指定相同数量和类型的备份设备。  
  
## <a name="example"></a>示例  
 下例创建上一图中所述的镜像介质集并将 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 数据库同时备份到两个镜像。  
  
```  
BACKUP DATABASE AdventureWorks2012  
TO TAPE = '\\.\tape0', TAPE = '\\.\tape1'  
MIRROR TO TAPE = '\\.\tape2', TAPE = '\\.\tape3'  
WITH  
    FORMAT,  
    MEDIANAME = 'AdventureWorks2012Set1';  
GO  
```  
  
## <a name="related-tasks"></a>Related Tasks  
 **从镜像备份还原**  
  
-   [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
## <a name="see-also"></a>请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [镜像备份媒体集 (SQL Server)](mirrored-backup-media-sets-sql-server.md)  
  
  
