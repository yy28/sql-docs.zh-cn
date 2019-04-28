---
title: 选择数据库页 （新建可用性组向导 / 添加数据库向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.adddatabasewizard.selectdatabases.f1
- sql12.swb.newagwizard.selectdatabases.f1
ms.assetid: 929c5e15-d087-438d-b1f2-aa97c5f8bff8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a2c6cdeb27dfd1768c9a494497f5b2b1e0b7350a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788483"
---
# <a name="select-databases-page-new-availability-group-wizard-add-database-wizard"></a>选择数据库页 （新建可用性组向导 / 添加数据库向导）
  本帮助主题说明 **“指定数据库”** 页的选项。 本主题适用于 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 的 [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] 和 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]。  
  
##  <a name="PageOptions"></a> 选择数据库选项  
 **“此 SQL Server 实例上的用户数据库”** 网格列出每个本地用户数据库。 这些列如下所示：  
  
 **名称**  
 显示本地用户数据库的名称。  
  
 **大小**  
 显示数据库大小（如果在该向导中提供）。  
  
 **“状态”**  
 显示超链接，其中的文本指示给定的数据库是否满足添加到可用性组的先决条件。 如果状态为 **“满足先决条件”**，则可以将该数据库添加到可用性组。 如果数据库不满足所有先决条件， **“状态”** 超链接将提供关于该数据库为何不符合要求的简短解释。 有关详细信息，请单击该超链接。  
  
 在对数据库采取操作以满足先决条件的过程中，您可以在 **“选择数据库”** 页上离开该向导。 当您返回 **“选择数据库”** 页时，请单击 **“刷新”** 更新该网格。  
  
 **刷新**  
 单击以刷新该网格。 对数据库采取操作以满足先决条件后，这样做非常有用。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [使用“新建可用性组”对话框 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [使用“将数据库添加到可用性组向导”(SQL Server Management Studio)](availability-group-add-database-to-group-wizard.md)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [先决条件、 限制和建议为 AlwaysOn 可用性组&#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)  
  
  
