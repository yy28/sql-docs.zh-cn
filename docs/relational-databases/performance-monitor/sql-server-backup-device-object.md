---
title: SQL Server - Backup Device 对象 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 87cda19087f0e1ed742399032888a77f2a013dd4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85787342"
---
# <a name="sql-server-backup-device-object"></a>SQL Server Backup Device 对象
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Backup Device** 对象提供的计数器可监视用于备份和还原操作的 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份设备。 在希望基于每个设备确定吞吐量或备份和还原操作的进度及性能时，可以监视备份设备。 若要监视整个数据库备份或还原操作的吞吐量，请使用  **Databases 对象的 Backup/Restore Throughput/sec 计数器**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  。 有关详细信息，请参阅 [SQL Server, Databases Object](../../relational-databases/performance-monitor/sql-server-databases-object.md)。  
  
 下表介绍 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份设备计数器  。  
  
|SQL Server Backup Device 计数器|说明|  
|---------------------------------------|-----------------|  
|**Device Throughput Bytes/sec**|一个备份设备在备份或还原数据库时所用的读写操作的吞吐量（以每秒字节数表示）。 这一计数器只有在备份或还原操作执行时才存在。|  
  
## <a name="see-also"></a>另请参阅  
 [备份设备 (SQL Server)](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
