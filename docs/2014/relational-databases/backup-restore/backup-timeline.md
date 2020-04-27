---
title: 备份时间线 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.POINTINTIMERESTORE.F1
- sql12.swb.backuptimeline.f1
helpviewer_keywords:
- Backup Timeline
ms.assetid: ae3565f2-ddb2-4469-a992-7531d4f9ebb8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 92cffa7c280aac559433a8fc7ad5a3223c9f6de2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62876699"
---
# <a name="backup-timeline"></a>备份时间线
  使用“备份时间线”  对话框可以查找和指定备份以便将数据库还原到某个时间点。 通过单击“还原数据库（“常规”页）”  窗格上的“时间线”  可以访问“备份时间线”  对话框。 通过此对话框，您可以查看对数据库执行的还原操作的时间线。  
  
 数据库恢复顾问确保仅选择需要恢复到该时点的那些备份。 这些选定的备份构成了为您的还原操作建议的还原计划。 您应仅使用选定的备份。 有关数据库恢复顾问的信息，请参阅[还原和恢复概述 (SQL Server)](restore-and-recovery-overview-sql-server.md)。  
  
## <a name="restore-to"></a>还原到  
 默认情况下，将选择 **“上次所做备份”** 。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 将选择相应的备份以便还原数据库，并且将数据库还原到该时点的上一备份。 单击“具体日期和时间”  可以手动设置日期和时间（选择特定的时间点）。  
  
 **“特定日期和时间”** 允许您停止在所选的特定日期和时间上的还原。 时间线展现了围绕所选日期和时间的 24 小时中执行的备份操作。  
  
 **Date**  
 输入一个日期或者从下拉列表中选择一个日期。  
  
 **时间**  
 输入或选择一个日期以便为还原停止指定特定的时间点。  
  
 **时间线间隔**  
 显示可在时间线上查看的间隔类型的选项。  
  
## <a name="timeline-and-legend"></a>时间线和图例  
 使用时间线之下的滚动条，沿时间线向前和向后移动光标。 单击某一备份以便将滚动条移动到该备份的结尾处。 将鼠标指针悬停在标记之上，以便显示提供与所选备份集有关的信息的屏幕提示。 备份信息通过以下标记显示在时间线上。  
  
 大三角形  
 表示对数据库执行的完全备份，同时指示执行每个完整备份的特定时间点。  
  
 小三角形  
 表示对数据库执行的差异备份，同时指示执行每个差异备份的特定时间点。  
  
 绿色阴影区域  
 表示事务日志备份覆盖范围。  
  
 红线  
 只能沿着可能执行还原的时间线定位。 沿时间线移动红线将调整在 **“日期”** 和 **“时间”** 框中显示的日期和时间。  
  
## <a name="see-also"></a>另请参阅  
 [还原数据库（“常规”页）](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
