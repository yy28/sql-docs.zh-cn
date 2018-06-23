---
title: 将数据和日志文件放到不同的驱动器上 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 6cbedc27-4d77-44ad-bed2-c23b628475a7
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 15cef6ec95e32d1eb086f7695b8f62e314cbc65c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015663"
---
# <a name="place-data-and-log-files-on-separate-drives"></a>将数据和日志文件放到不同的驱动器上
  此规则检查是否将数据和日志文件放到了不同的逻辑驱动器上。 将数据和日志文件放到同一个设备上会导致该设备的争用，并且会导致性能降低。 将文件放到不同的驱动器上允许数据和日志文件的 I/O 活动同时发生。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 创建新的数据库时，为数据和日志指定不同的驱动器。 若要在创建数据库后移动文件，则必须使数据库脱机。 使用以下方法之一移动文件：  
  
> [!NOTE]  
>  此策略无法通过装入点检测分开的物理设备。  
  
-   使用具有 WITH MOVE 选项的 RESTORE DATABASE 语句从备份还原数据库。  
  
-   通过为数据和日志设备指定不同的位置来分离然后附加数据库。  
  
-   指定新位置，方法是运行具有 MODIFY FILE 选项的 ALTER DATABASE 语句，然后重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。  
  
## <a name="for-more-information"></a>有关详细信息  
 [移动数据库文件](../databases/move-database-files.md)  
  
 [移动用户数据库](../databases/move-user-databases.md)  
  
 [数据库分离和附加 (SQL Server)](../databases/database-detach-and-attach-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  