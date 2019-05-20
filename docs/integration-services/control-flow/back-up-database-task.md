---
title: “备份数据库”任务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.backupdatabasetask.f1
helpviewer_keywords:
- database backups [Integration Services]
- Back Up Database task [Integration Services]
- backing up databases [Integration Services]
- transaction log backups [Integration Services]
- backing up transaction logs [Integration Services]
ms.assetid: b8839d71-13b7-41f2-a434-cb95020e79d7
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b8e4fee484f3302b72c1cfc3da9f0e4e62cae5a0
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2019
ms.locfileid: "65727977"
---
# <a name="back-up-database-task"></a>“备份数据库”任务

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  “备份数据库”任务可执行不同类型的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库备份。 有关详细信息，请参阅 [Back Up and Restore of SQL Server Databases](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)。  
  
 通过使用“备份数据库”任务，包可以备份单个数据库或多个数据库。 如果此任务仅备份单个数据库，则可以选择备份组件：数据库或者其文件和文件组。  
  
## <a name="supported-recover-models-and-backup-types"></a>支持的恢复模式和备份类型  
 下表列出了“备份数据库”任务支持的恢复模式和备份类型。  
  
|恢复模式|“数据库”|数据库差异|事务日志|文件或文件差异|  
|--------------------|--------------|---------------------------|---------------------|-------------------------------|  
|Simple|Required|可选|不支持|不支持|  
|完全|Required|可选|Required|可选|  
|大容量日志|Required|可选|Required|可选|  
  
 “备份数据库”任务封装 Transact-SQL BACKUP 语句。 有关详细信息，请参阅 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)。  
  
## <a name="configuration-of-the-back-up-database-task"></a>“备份数据库”任务的配置  
 可以通过 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器来设置属性。 此任务位于 **设计器中** “工具箱” **的** “维护计划中的任务” [!INCLUDE[ssIS](../../includes/ssis-md.md)] 部分。  
  
 有关可在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置的属性的详细信息，请单击以下主题：  
  
-   [“备份数据库”任务（维护计划）](../../relational-databases/maintenance-plans/options-in-the-back-up-database-task-for-maintenance-plan.md)  
  
 有关如何在 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 设计器中设置这些属性的详细信息，请单击下列主题：  
  
-   [设置任务或容器的属性](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
  
