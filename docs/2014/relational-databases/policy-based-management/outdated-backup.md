---
title: 过时的备份 | Microsoft Docs
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
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 702d49974dc77aad02b9cf79a1ebeff2ed03dc25
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124072"
---
# <a name="outdated-backup"></a>过时的备份
  此规则检查数据库是否有最新备份。 计划定期备份对于防止数据库因多种不同故障而造成数据丢失很重要。 用于备份数据的合适频率取决于数据库的恢复模式、有关可能数据丢失的业务需求以及数据库的更新频率。 在频繁更新的数据库中，两次备份之间丢失工作的风险增加得相当快。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 建议您经常执行备份，以防止数据库丢失数据。  
  
 简单恢复模式和完整恢复模式都需要数据备份。 对于任意一种恢复模式，您都可以使用差异备份来补充完整备份，以便有效地降低数据丢失的风险。  
  
 对于使用完整恢复模式的数据库，建议您经常进行日志备份。 对于包含非常重要数据的生产数据库，通常每隔 1 到 15 分钟进行一次日志备份。  
  
> [!NOTE]  
>  计划备份的推荐方法是数据库维护计划。  
  
## <a name="for-more-information"></a>有关详细信息  
 [备份和还原系统数据库 (SQL Server)](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [恢复模式 (SQL Server)](../backup-restore/recovery-models-sql-server.md)  
  
 [创建差异数据库备份 (SQL Server)](../backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [创建完整数据库备份 (SQL Server)](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [维护计划](../maintenance-plans/maintenance-plans.md)  
  
 [事务日志备份 (SQL Server)](../backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  