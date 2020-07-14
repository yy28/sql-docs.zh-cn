---
title: 将数据和日志文件放到不同的驱动器上 | Microsoft Docs
description: 将数据和日志文件放到不同的逻辑驱动器上。 放在不同的位置后，每个位置的活动可同时发生，从而提高 SQL 性能。
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7c0ed515a8fe166d4b53fec5750fa3b09a48a06a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716853"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>将数据和日志文件放到不同的驱动器上
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  此规则检查是否将数据和日志文件放到了不同的逻辑驱动器上。 将数据和日志文件放到同一个设备上会导致该设备的争用，导致性能降低。 将文件放到不同的驱动器上允许数据和日志文件的 I/O 活动同时发生。  
  
## <a name="recommendations"></a>建议  
 创建新的数据库时，为数据和日志指定不同的驱动器。 若要在创建数据库后移动文件，则必须使数据库脱机。 使用下列方法之一移动文件：  
  
> [!NOTE]  
>  此策略无法通过装入点检测分开的物理设备。  
  
-   使用具有 WITH MOVE 选项的 RESTORE DATABASE 语句从备份还原数据库。  
  
-   通过为数据和日志设备指定不同的位置来分离然后附加数据库。  
  
-   指定新位置，方法是运行具有 MODIFY FILE 选项的 ALTER DATABASE 语句，然后重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
## <a name="for-more-information"></a>有关详细信息  
 [移动数据库文件](../../relational-databases/databases/move-database-files.md)  
  
 [移动用户数据库](../../relational-databases/databases/move-user-databases.md)  
  
 [数据库分离和附加 (SQL Server)](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳做法](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
