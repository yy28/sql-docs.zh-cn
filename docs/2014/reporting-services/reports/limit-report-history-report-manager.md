---
title: 限制报表历史记录（报表管理器）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- viewing report history
- report history [Reporting Services], viewing history
- report history [Reporting Services], configuring history
- historical data [Reporting Services]
- displaying report history
ms.assetid: 8e255792-d9ef-496f-a26c-9e969c1209a0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d6f4508dda8496d9065655f5a8e298feaa4e9ad3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48134027"
---
# <a name="limit-report-history-report-manager"></a>限制报表历史记录（报表管理器）
  报表历史记录是随着时间变化而创建的报表快照的集合。 您可以按需创建报表历史记录，也可以安排快照的创建频率以及将快照添加到报表历史记录中的频率。  
  
 报表历史记录存储在报表服务器数据库中。 如果报表快照中包含大量数据，则可以考虑限制报表历史记录，以便尽可能减少快照保持期对数据库大小的影响。  
  
### <a name="to-configure-report-history-for-a-report-server"></a>为报表服务器配置报表历史记录  
  
1.  在报表管理器中，单击全局工具栏上的 **“站点设置”** 。  
  
2.  如果希望无限制地保留所有报表历史记录，请选择 **“不限制报表历史记录中保留的快照数”** 。 否则，请选择 **“限制报表历史记录的副本数”** ，以指定可以为任何给定报表保留的最多快照数。  
  
3.  单击 **“应用”**。  
  
### <a name="to-configure-report-history-for-a-specific-report"></a>为特定的报表配置报表历史记录  
  
1.  在报表管理器中，导航到要配置历史记录的报表，再单击该报表将其打开。  
  
2.  单击 **“属性”** 选项卡。  
  
3.  单击 **“历史记录”** 选项卡。  
  
4.  为您的报表选择相应选项，再单击 **“应用”**。 有关每个选项的详细信息，请参阅[“快照选项”属性页（报表管理器）](../snapshot-options-properties-page-report-manager.md)。  
  
## <a name="see-also"></a>请参阅  
 [将快照添加到报表历史记录&#40;报表管理器&#41;](../report-server/add-a-snapshot-to-report-history-report-manager.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)  
  
  
