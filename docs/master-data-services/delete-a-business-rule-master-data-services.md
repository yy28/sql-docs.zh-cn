---
title: "删除业务规则 (Master Data Services) | Microsoft Docs"
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
  - "删除业务规则 [Master Data Services]"
  - "业务规则 [Master Data Services], 删除"
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 删除业务规则 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，当不再需要某个业务规则时，可以删除它。  
  
> [!NOTE]  
>  您可以通过排除业务规则而不是删除它来防止针对业务规则验证数据。 有关详细信息，请参阅[排除业务规则 (Master Data Services)](../master-data-services/exclude-a-business-rule-master-data-services.md)。  
  
## 先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### 删除业务规则  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在“业务规则”页上，从“模型”下拉列表中选择一个模型。  
  
4.  从“实体”下拉列表中选择一个实体。  
  
5.  从“成员类型”下拉列表中，选择要应用业务规则的成员类型。  
  
6.  在网格中，单击要删除的业务规则所对应的行。  
  
7.  单击 **“删除”**。  
  
8.  在确认对话框中，单击 **“确定”**。 “业务规则状态”  列中的值为“待删除” 。  
  
9. 单击“全部发布” 。  
  
10. 在确认对话框中，单击 **“确定”**。 已删除的业务规则不会再显示在网格中。  
  
## 另请参阅  
 [排除业务规则 (Master Data Services)](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [创建和发布业务规则 (Master Data Services)](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [业务规则 (Master Data Services)](../master-data-services/business-rules-master-data-services.md)  
  
  