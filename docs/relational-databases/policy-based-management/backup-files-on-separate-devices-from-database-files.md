---
title: 备份文件与数据库文件必须位于不同的设备上
description: 了解如何针对 SQL Server 基于策略的管理来启用策略，以检查备份文件和数据库文件的位置。
ms.custom: seo-lt-2019
ms.date: 08/31/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
author: dzsquared
ms.author: drskwier
ms.openlocfilehash: 5b98f8163a3564ccc4aadac6c71c30eb5cf37697
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/01/2020
ms.locfileid: "89284945"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>备份文件与数据库文件必须位于不同的设备上
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此规则检查数据库文件是否位于与备份文件分开的设备上。 如果数据库文件和备份文件位于同一台设备上并且该设备出现故障，数据库和备份都将不可用。 此外，将数据库和备份文件放到不同的设备上还可以优化使用数据库和写入备份时的 I/O 性能。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 我们建议备份磁盘应不同于数据库数据和日志的磁盘。 这是数据或日志磁盘出现故障时访问备份数据必不可少的。

如果数据库文件和备份文件位于同一台设备上并且该设备出现故障，数据库和备份都将不可用。 此外，将数据库和备份文件放到不同的设备上还可以优化使用数据库和写入备份时的 I/O 性能。
  
## <a name="see-also"></a>另请参阅 
   
  
 [备份设备](../backup-restore/backup-devices-sql-server.md)  
  
