---
title: 暂停报表和订阅处理 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1607637630c507588602dd7e566917ce1eeb6080
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100915"
---
# <a name="pause-report-and-subscription-processing"></a>暂停报表和订阅处理
  您不能直接暂停报表或订阅。 不过，在报表和订阅处理进程启动之前或者在建立数据源连接时，您可以中断报表和订阅处理。 您还可以通过使用户不能访问报表或订阅，来阻止对报表或订阅进行处理。  
  
 您可以使用以下策略暂时阻止进行处理。  
  
## <a name="modify-role-assignments-to-prevent-access"></a>通过修改角色分配来阻止访问  
 使报表不可用的最佳方法是，暂时删除提供报表访问权限的角色分配。 无论采用哪种数据源连接，对所有报表都可以使用这种方法。 这种方法只针对目标报表，不会影响其他报表或项的操作。  
  
 若要删除角色分配，请在报表管理器中打开报表的“安全属性”页。 如果报表的安全设置是从父报表继承来的，则可以单击“编辑项安全设置”****，创建一个忽略提供大范围访问权的角色分配的限制性安全策略。例如，可以删除为 Everyone 提供访问权的角色分配，而保留为一组少量用户（如 Administrators）提供访问权的角色分配。  
  
## <a name="disable-a-shared-data-source"></a>禁用共享数据源  
 使用共享数据源的一个优点是您可以通过禁用它来阻止报表或数据驱动订阅运行。 禁用共享数据源会断开报表与其外部源的连接。 禁用共享数据源后，所有原来使用该数据源的报表和订阅将无法再继续访问该数据源。 若要禁用共享数据源，请在报表管理器中打开相应的数据源，再清除 **“启用此数据源”** 复选框。  
  
 请注意，即使数据源不可用，您也仍可加载相应的报表。 该报表不包含任何数据，但具有适当权限的用户可以访问与该报表关联的属性页、安全设置、报表历史记录和订阅信息。  
  
## <a name="pause-a-shared-schedule"></a>暂停共享计划  
 如果报表或订阅按照某个共享计划运行，您可以通过暂停该计划来阻止这些报表或订阅的处理。 在恢复计划之前，会延迟由该计划驱动的所有报表和订阅处理。 有关详细信息，请参阅[暂停和恢复共享计划](schedules.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Reporting Services 报表服务器 &#40;本机模式&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [报表管理器（SSRS 本机模式）](../report-manager-ssrs-native-mode.md)   
 ["安全属性" 页，项 &#40;报表管理器&#41;](../security-properties-page-items-report-manager.md)  
  
  
