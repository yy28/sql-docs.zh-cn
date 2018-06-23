---
title: 创建报表历史记录（SharePoint 集成模式下的 Reporting Services）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- report history [Reporting Services], SharePoint
ms.assetid: e57ec746-05ae-4ff6-8e39-6cde87310daa
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: e5f06beea8a9aeb9d5ec3d0761d2360b45c3d7ec
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36128920"
---
# <a name="create-report-history-reporting-services-in-sharepoint-integrated-mode"></a>创建报表历史记录（SharePoint 集成模式下的 Reporting Services）
  报表历史记录是随着时间变化而创建的报表快照的集合。 每个快照都是报表创建时所生成的报表的副本。 它包含创建快照时该报表当时的布局和数据。 呈现信息不与快照存储在一起。 打开报表历史记录中的快照时，它将在报表查看器 Web 部件中以 HTML 形式打开。 呈现该快照后，您可以将其导出为其他应用程序格式。  
  
 若要创建报表历史记录，报表必须能够以无人参与的形式运行（也就是说，报表服务器必须能够在没有用户交互的情况下运行报表）。 必须对包含报表的库拥有“编辑项”权限。 若要查看或删除报表历史记录，您必须拥有“查看版本”或“删除版本”权限。  
  
### <a name="to-create-a-snapshot-or-report-history-on-demand"></a>按需创建快照或报表历史记录  
  
1.  指向报表。  
  
2.  单击以显示下箭头，然后选择 **“查看报表历史记录”**。  
  
3.  单击 **“新建快照”**。 如果该按钮不可见，则是因为您没有在报表历史记录中创建快照的权限。  
  
4.  若要查看您刚创建的快照，从列表中将其选中。 每个快照都是由用来显示何时创建快照的时间戳进行标识的。 您不能重命名快照，不能将其移动到另一个位置，也不能修改它。  
  
### <a name="to-schedule-report-history"></a>计划报表历史记录  
  
1.  指向报表。  
  
2.  单击以显示下箭头，然后选择 **“管理处理选项”**。  
  
3.  在 **“历史记录快照选项”** 中，单击 **“根据计划创建报表历史记录快照”**。  
  
4.  如果您有包含要使用的计划信息的共享计划，请单击 **“根据共享计划”** 并选择要使用的计划。 否则，请单击 **“根据自定义计划”**，然后单击 **“配置”** 以指定根据重复执行的计划来创建报表历史记录的选项。  
  
### <a name="to-create-report-history-when-data-is-refreshed-in-a-report"></a>在刷新报表中的数据时创建报表历史记录  
  
1.  指向报表。  
  
2.  单击以显示下箭头，然后选择 **“管理处理选项”**。  
  
3.  在 **“历史记录快照选项”** 中，单击 **“在报表历史记录中存储所有报表数据快照”**。  
  
## <a name="see-also"></a>请参阅  
 [设置处理选项（SharePoint 集成模式下的 Reporting Services）](../set-processing-options-reporting-services-in-sharepoint-integrated-mode.md)  
  
  