---
title: "过时的备份 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: performance-monitor
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Best Practices [Database Engine]
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce4d4891a2d48bd59dbd94025d55204540efc94c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="outdated-backup"></a>过时的备份
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]此规则检查数据库是否有最新备份。 计划定期备份对于防止数据库因多种不同故障而造成数据丢失很重要。 用于备份数据的合适频率取决于数据库的恢复模式、有关可能数据丢失的业务需求以及数据库的更新频率。 在频繁更新的数据库中，两次备份之间丢失工作的风险增加得相当快。  
  
## <a name="best-practices-recommendations"></a>最佳做法建议  
 建议您经常执行备份，以防止数据库丢失数据。  
  
 简单恢复模式和完整恢复模式都需要数据备份。 对于任意一种恢复模式，您都可以使用差异备份来补充完整备份，以便有效地降低数据丢失的风险。  
  
 对于使用完整恢复模式的数据库，建议您经常进行日志备份。 对于包含非常重要数据的生产数据库，通常每隔 1 到 15 分钟进行一次日志备份。  
  
> [!NOTE]  
>  计划备份的推荐方法是数据库维护计划。  
  
## <a name="for-more-information"></a>有关详细信息  
 [备份和还原系统数据库 (SQL Server)](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [恢复模式 (SQL Server)](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
 [创建差异数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [创建完整数据库备份 (SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [维护计划](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
 [事务日志备份 (SQL Server)](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用基于策略的管理来监视和强制执行最佳实践](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
