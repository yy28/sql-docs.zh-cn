---
title: "创建模型 (Master Data Services) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- models [Master Data Services], creating models
- creating models [Master Data Services]
ms.assetid: 9bb3b3b3-bde8-44aa-ad62-eaae21188141
caps.latest.revision: 13
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 1a32cc8f778496f5609d44c17b69623b75b8c240
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="create-a-model-master-data-services"></a>创建模型 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，创建模型以便包含模型对象。  
  
## <a name="prerequisites"></a>先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### <a name="to-create-a-model"></a>创建模型  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“模型”**。  
  
3.  在“管理模型”  页上，单击“添加” 。 面板将会在右侧显示。  
  
4.  在“名称”  框中，键入模型的名称。  
  
5.  （可选）在“说明”字段中，输入模型说明。  
  
6.  在“日志保留天数”  字段中，选择一个选项来保留日志数据。 默认值是“系统设置” ，指示值继承自 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中的系统设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](../master-data-services/system-settings-master-data-services.md)。  
  
     若要替代系统设置且不删除事务日志数据，请选择“否” 。 若要仅保留今日的日志数据并截断之前所有天数的日志数据，请选择“是”  并将“天数”  字段设置为 0。 若要保留特定天数的日志数据，请选择“是”  并将“天数”  字段设置为相应天数。  
  
7.  或者，选择 **“使用与模型相同的名称创建实体”** 可以使用与模型相同的名称创建实体。  
  
8.  单击 **“保存模型”**。  
  
 对于创建的每个模型，系统都会在网格中添加一行（其中包含八列）。 八个列是：  
  
-   状态：模型状态。 单击“保存模型”按钮后，系统会显示![正在更新](../master-data-services/media/mds-model-status-updating.png "Updating")图像，表示模型正在更新。 如果创建或编辑模型时出现错误，系统会显示![错误](../master-data-services/media/mds-model-status-error.png "Error")图像。 否则，如果状态为“正常”，会显示 ![“确定”](../master-data-services/media/mds-model-status-ok.png "“确定”") 图像。  
  
-   名称：模型名称。  
  
-   说明：模型说明。  
  
-   日志保留天数：日志可保留该模型的天数。  
  
-   创建者：创建模型的用户的用户名。  
  
-   创建的日期和时间：创建模型的日期和时间。  
  
-   更新者：上次更新模型的用户的用户名。  
  
-   创建的日期和时间：上次更新模型的日期和时间。  
  
## <a name="next-steps"></a>后续步骤  
  
-   [创建实体 (Master Data Services)](../master-data-services/create-an-entity-master-data-services.md)  
  
## <a name="see-also"></a>另请参阅  
 [模型 (Master Data Services)](../master-data-services/models-master-data-services.md)   
 [实体 (Master Data Services)](../master-data-services/entities-master-data-services.md)   
 [删除模型 &#40;Master Data Services&#41;](../master-data-services/delete-a-model-master-data-services.md)   
 [编辑模型 &#40;Master Data Services&#41;](../master-data-services/edit-model-master-data-services.md)   
 [事务 (Master Data Services)](../master-data-services/transactions-master-data-services.md)  
  
  
