---
title: "重叠的模型和成员权限（主数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "模型 [Master Data Services], 有效权限"
  - "权限 [Master Data Services], 模型和成员重叠"
  - "成员 [Master Data Services], 有效权限"
ms.assetid: 9fd7a555-43bf-4796-a8b6-1ca63a291216
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# 重叠的模型和成员权限（主数据服务）
  分配给成员的权限可与分配给模型对象的权限重叠。 出现重叠时，限制性更强的权限将生效。  
  
 如果成员具有不同于其相应模型对象的权限，适用以下规则：  
  
-   **“拒绝”** 覆盖所有其他权限。  
  
-   **管理员** 模型级别权限覆盖所有其他权限，并将更改为子级别上的所有 (CRUD) 访问权限。  
  
-   有效访问权限与成员和属性权限相交。  
  
     例如，如果成员权限包括 **“创建”** 和 **“更新”**，则属性的权限是 **“更新”**。 有效权限是 **“更新”**。  
  
 下图显示在属性权限不同于成员权限时，哪些权限对单个属性值有效。  
  
 ![mds_conc_security_member_overlap_table](../master-data-services/media/mds-conc-security-member-overlap-table.gif "mds_conc_security_member_overlap_table")  
  
## 示例 1  
 ![mds_conc_overlap_model_1](../master-data-services/media/mds-conc-overlap-model-1.gif "mds_conc_overlap_model_1")  
  
 在 **“模型”** 选项卡上，Product 实体分配有 **“更新”** 权限。 该实体中的所有属性都继承该权限。  
  
 在 **“层次结构成员”** 选项卡上，派生的层次结构中的“山地车”子类别节点分配有 **“更新”** 权限。  
  
 结果：在 **“资源管理器”**中，用户对“山地车”节点中所有成员的所有属性值都具有 **“更新”** 权限。 所有其他成员和属性均隐藏。  
  
 ![mds_conc_overlap_model_example_1](../master-data-services/media/mds-conc-overlap-model-example-1.gif "mds_conc_overlap_model_example_1")  
  
## 示例 2  
 ![mds_conc_overlap_model_2](../master-data-services/media/mds-conc-overlap-model-2.gif "mds_conc_overlap_model_2")  
  
 在 **“模型”** 选项卡上，Subcategory 属性分配有 **“更新”** 权限。  
  
 在 **“层次结构成员”** 选项卡上，派生的层次结构中的“山地车”子类别节点显式分配有 **“读取”** 权限。  
  
 结果：在 **“资源管理器”**中，用户对“山地车”节点中的成员的所有 Subcategory 属性值都具有 **“读取”** 权限。 所有其他成员和属性均隐藏。  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## 示例 3  
 ![mds_conc_overlap_model_3](../master-data-services/media/mds-conc-overlap-model-3.gif "mds_conc_overlap_model_3")  
  
 在 **“模型”** 选项卡上，Subcategory 属性分配有 **“读取”** 权限。  
  
 在 **“层次结构成员”** 选项卡上，派生的层次结构中的“山地车”子类别显式分配有 **“更新”** 权限。  
  
 结果：在 **“资源管理器”**中，用户对这些属性值具有 **“读取”** 权限。 所有其他成员和属性均隐藏。  
  
 ![mds_conc_overlap_model_example_2](../master-data-services/media/mds-conc-overlap-model-example-2.gif "mds_conc_overlap_model_example_2")  
  
## 另请参阅  
 [如何确定权限 & #40;Master Data Services & #41;](../master-data-services/how-permissions-are-determined-master-data-services.md)   
 [重叠的用户和组权限和 #40;Master Data Services & #41;](../master-data-services/overlapping-user-and-group-permissions-master-data-services.md)  
  
  