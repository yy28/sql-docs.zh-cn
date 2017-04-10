---
title: "删除模型 (Master Data Services) | Microsoft Docs"
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
  - "删除模型 [Master Data Services]"
  - "模型 [Master Data Services], 删除模型"
ms.assetid: f0ad3cc4-aed7-47c8-94bc-2971fe9fe871
caps.latest.revision: 6
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 6
---
# 删除模型 (Master Data Services)
  删除一个模型将从 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中删除该模型及其所有数据。  
  
> [!NOTE]  
>  完成此过程后，将从该模型的所有版本中永久删除所有对象和所有数据。  
  
## 先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### 删除模型  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  在 **“模型视图”** 页上，从菜单栏中，指向 **“管理”** ，然后单击 **“模型”**。  
  
3.  在“管理模型”页上，从网格中选择要删除的模型所在的行。   
  
4.  单击 **“删除”**。  
  
5.  在确认对话框中，单击 **“确定”**。  
  
6.  在附加确认对话框中，单击 **“确定”**。  
  
 网格的“状态”列中显示了对模型所执行操作的状态。  单击“保存模型”按钮后，系统会显示 ![Updating](../master-data-services/media/mds-model-status-updating.png "Updating") 图像，指明正在更新模型。 如果在创建或编辑模型时出错，系统会显示 ![Error](../master-data-services/media/mds-model-status-error.png "Error") 图像。 否则，如果状态为“正常”，会显示 ![OK](../master-data-services/media/mds-model-status-ok.png "OK") 图像。  
  
## 另请参阅  
 [模型 (Master Data Services)](../master-data-services/models-master-data-services.md)   
 [创建模型 (Master Data Services)](../master-data-services/create-a-model-master-data-services.md)  
  
  