---
title: "要求属性值 (Master Data Services) | Microsoft Docs"
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
  - "业务规则 [Master Data Services], 要求属性值"
  - "属性 [Master Data Services], 要求值"
ms.assetid: a360ef13-0c34-43b8-a87e-2f5d8732d30e
caps.latest.revision: 9
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 9
---
# 要求属性值 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，在您想要确保主数据完整时要求属性值。  
  
> [!NOTE]  
>  缺少基于域的属性值的成员不显示在基于那些关系的派生层次结构中。  
  
## 先决条件  
 若要执行此过程：  
  
-   您必须有权访问 **“系统管理”** 功能区域。  
  
-   您必须是模型管理员。 有关详细信息，请参阅 [管理员和 #40;Master Data Services & #41;](../master-data-services/administrators-master-data-services.md)。  
  
### 要求属性值  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，单击 **“系统管理”**。  
  
2.  从菜单栏中，指向 **“管理”** ，然后单击 **“业务规则”**。  
  
3.  在 **业务规则** 页上，从 **模型** 下拉列表中选择一个模型。  
  
4.  从 **实体** 下拉列表中，选择一个实体。  
  
5.  从 **Member Types** 下拉列表中选择要将应用于的业务规则的成员类型的一个。  
  
6.  单击 **“添加”**。  
  
7.  在“名称”  框中，键入业务规则的名称。  
  
8.  （可选）在“说明”  字段中，键入业务规则描述。  
  
9. 在“Then”  块下，单击“添加” 。 此时将显示一个面板。  
  
10. 从 **运算符** 下拉列表中，选择 **必需操作**。  
  
11. 从 **属性** 下拉列表中，选择一种属性。  
  
12. 单击 **“保存”**。 此时，系统会在“Then”  网格中新添加一行。  
  
13. 单击 **“保存”**。  
  
14. 单击“全部发布” 。  
  
15. 在确认对话框中，单击 **“确定”**。 “业务规则状态”  列中的值为“有效” 。  
  
## 后续步骤  
  
-   通过以下过程之一将业务规则应用到数据：  
  
    -   [针对业务规则和 #40; 验证特定成员Master Data Services & #41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
    -   [针对业务规则和 #40; 验证版本Master Data Services & #41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)  
  
## 另请参阅  
 [业务规则和 #40;Master Data Services & #41;](../master-data-services/business-rules-master-data-services.md)   
 [派生层次结构 & #40;Master Data Services & #41;](../master-data-services/derived-hierarchies-master-data-services.md)  
  
  