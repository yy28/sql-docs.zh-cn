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
ms.openlocfilehash: 255a3c190139c029f5211dcab9780b6d07d975a4
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84959487"
---
# <a name="back-up-to-a-mirrored-media-set-transact-sql"></a>备份镜像媒体集 (Transact-SQL)
  本主题介绍 [!INCLUDE[tsql](../../includes/tsql-md.md)] 在备份数据库时如何使用[BACKUP](/sql/t-sql/statements/backup-transact-sql)语句指定镜像介质集 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 。 在 BACKUP 语句中的 TO 子句中指定第一个镜像。 然后，在它自己的 MIRROR TO 子句中指定每个镜像。 TO 和 MIRROR TO 子句必须指定相同数量和类型的备份设备。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [镜像备份媒体集 (SQL Server)](mirrored-backup-media-sets-sql-server.md)  
  
  
