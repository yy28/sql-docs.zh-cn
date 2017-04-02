---
title: "编辑模型 (Master Data Services) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "模型 [Master Data Services]，更改名称"
ms.assetid: 399eed32-7c61-4239-9c06-996a65219518
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# 编辑模型 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，你可以更改模型的名称和说明，并指明所需的事务日志保留期（以天为单位）。  
  
 有关详细信息，请参阅[事务 (Master Data Services)](../master-data-services/transactions-master-data-services.md)。  
  
## 先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### 更改模型  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“模型”**。  
  
3.  在“管理模型”  页上，从网格中选择要更改其名称或说明的模型所在的行。  
  
4.  单击 **“编辑”**。  
  
5.  在“名称”  框中，键入更新后的模型名称。  
  
6.  在“说明”  字段中，键入更新后的模型说明。  
  
7.  在“日志保留期(以天为单位)”  字段中，选择一个日志数据保留选项。 默认值是“系统设置” ，指示值继承自 [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)]中的系统设置。 有关详细信息，请参阅[系统设置 (Master Data Services)](../master-data-services/system-settings-master-data-services.md)。  
  
     若要替代系统设置且不删除事务日志数据，请选择“否” 。 若要仅保留今日的日志数据并截断之前所有天数的日志数据，请选择“是”  并将“天数”  字段设置为 0。 若要保留特定天数的日志数据，请选择“是”  ，然后将“天数”  字段设置为相应天数。  
  
8.  单击 **“保存模型”**。  
  
 网格的“状态”列中显示了对模型所执行操作的状态。  单击“保存模型”按钮后，系统会显示 ![Updating](../master-data-services/media/mds-model-status-updating.png "Updating") 图像，指明正在更新模型。 如果在创建或编辑模型时出错，系统会显示 ![Error](../master-data-services/media/mds-model-status-error.png "Error") 图像。 否则，如果状态为“正常”，会显示 ![OK](../master-data-services/media/mds-model-status-ok.png "OK") 图像。  
  
## 另请参阅  
 [创建模型 (Master Data Services)](../master-data-services/create-a-model-master-data-services.md)   
 [删除模型 (Master Data Services)](../master-data-services/delete-a-model-master-data-services.md)   
 [模型 (Master Data Services)](../master-data-services/models-master-data-services.md)  
  
  