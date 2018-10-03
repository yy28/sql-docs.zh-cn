---
title: 编辑模型 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology:
- master-data-services
ms.topic: conceptual
helpviewer_keywords:
- models [Master Data Services], changing name
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 64a3c2b613dfb13c10103f1663c55c58d653c306
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673521"
---
# <a name="edit-model-master-data-services"></a>编辑模型 (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，你可以更改模型的名称和说明，并指明所需的事务日志保留期（以天为单位）。  
  
 有关详细信息，请参阅[事务 (Master Data Services)](../master-data-services/transactions-master-data-services.md)。  
  
## <a name="prerequisites"></a>必备条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-change-a-model"></a>更改模型  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“模型”**。  
  
3.  在“管理模型”  页上，从网格中选择要更改其名称或说明的模型所在的行。  
  
4.  单击 **“编辑”**。  
  
5.  在“名称”  框中，键入更新后的模型名称。  
  
6.  在“说明”  字段中，键入更新后的模型说明。  
  
7.  在“日志保留期(以天为单位)”  字段中，选择一个日志数据保留选项。 默认值是“系统设置” ，指示值继承自 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中的系统设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](../master-data-services/system-settings-master-data-services.md)。  
  
     若要替代系统设置且不删除事务日志数据，请选择“否” 。 若要仅保留今日的日志数据并截断之前所有天数的日志数据，请选择“是”  并将“天数”  字段设置为 0。 若要保留特定天数的日志数据，请选择“是”  ，然后将“天数”  字段设置为相应天数。  
  
8.  单击 **“保存模型”**。  
  
 网格的“状态”列中显示了对模型所执行操作的状态。  单击“保存模型”按钮后，系统会显示![正在更新](../master-data-services/media/mds-model-status-updating.png "Updating")图像，表示模型正在更新。 如果创建或编辑模型时出现错误，系统会显示![错误](../master-data-services/media/mds-model-status-error.png "Error")图像。 否则，如果状态为“正常”，会显示 ![“确定”](../master-data-services/media/mds-model-status-ok.png "“确定”") 图像。  
  
## <a name="see-also"></a>另请参阅  
 [创建模型 (Master Data Services)](../master-data-services/create-a-model-master-data-services.md)   
 [删除模型 &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [模型 (Master Data Services)](../master-data-services/models-master-data-services.md)  
  
  
