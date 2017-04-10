---
title: "应用并更新变更集 (Master Data Services) | Microsoft Docs"
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
ms.assetid: 3a6a3cf2-1e77-43d3-a64a-855ae51258e7
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# 应用并更新变更集 (Master Data Services)
  变更集是主数据的挂起更改的集合。 可以在本地应用变更集以查看、添加、更新和删除变更集中挂起的更改。  
  
## 先决条件  
  
-    您必须有权访问“资源管理器”功能区域。 有关详细信息，请参阅[功能区域权限 (Master Data Services)](../master-data-services/functional-area-permissions-master-data-services.md)。  
  
-   你必须至少拥有实体或其属性之一的更新访问权限。  
  
-   如果你是实体管理员，只可以查看你拥有的变更集或提交以供审核的变更集。  
  
-   在变更集处于打开或拒绝状态时，你仅可以修改自己拥有的变更集。  
  
## 应用并更新变更集  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页中，选择模型和版本，然后单击“资源管理器” 。  
  
2.  单击“实体”菜单中的某个实体  。  
  
3.  在右窗格中，选择“变更集”，然后双击你想要查看或更改的变更集。  
  
4.  单击 **“应用”**。  
  
     挂起的更改应用于网格中的实体成员。 挂起的更改会突出显示。  
  
     创建、删除和更新成员会导致变更集发生变化。  
  
5.  若要还原挂起的更改，右键单击“变更集”窗格中的网格，然后单击“还原”。  
  
## 后续步骤  
 [确认或提交变更 (Master Data Services)](../master-data-services/commit-or-submit-a-changeset-master-data-services.md)  
  
## 另请参阅  
 [创建变更集 (Master Data Services)](../master-data-services/create-a-changeset-master-data-services.md)   
 [批准或拒绝变更集 (Master Data Services)](../master-data-services/approve-or-reject-a-changeset-master-data-services.md)  
  
  