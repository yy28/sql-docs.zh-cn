---
title: "重新激活成员或集合 (Master Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "集合 [Master Data Services], 重新激活"
  - "合并成员 [Master Data Services], 重新激活"
  - "重新激活成员 [Master Data Services]"
  - "成员 [Master Data Services], 重新激活"
  - "重新激活集合 [Master Data Services]"
  - "叶成员 [Master Data Services], 重新激活"
ms.assetid: bb4884c0-3658-4763-92d1-636804278b1c
caps.latest.revision: 11
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 11
---
# 重新激活成员或集合 (Master Data Services)
  在 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]中，可以重新激活以下成员：  
  
-   这些成员已通过临时过程停用。  
  
-   已在 MDS [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]中删除这些成员。  
  
-   已在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] Web 应用程序中删除这些成员。  
  
 重新激活成员时，将还原成员的属性以及成员在层次结构和集合中的成员身份。  
  
 您还可以重新激活集合。 重新激活集合时，将还原集合的属性和集合中的成员。  
  
 重新激活集合或成员时，将还原以前的所有事务。  
  
## 先决条件  
 若要执行此过程：  
  
-   在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]中，您必须具有对 **“版本管理”** 功能区域的权限。  
  
-   您必须是模型管理员。 有关详细信息，请参阅[管理员 (Master Data Services)](../master-data-services/administrators-master-data-services.md)。  
  
### 重新激活成员或集合  
  
1.  在 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 主页上，单击 **“版本管理”**。  
  
2.  在菜单栏上，单击 **“事务”**。  
  
3.  在 **“事务”** 页上，从 **“模型”** 列表中选择某个模型。  
  
4.   从“版本”列表中，选择某一版本。  
  
5.  在 **“事务”** 窗格中，单击要重新激活的成员或集合所对应的行。 此行应在“旧值”列中显示“活动”并在“新值”列中显示“已停用”。  
  
6.  单击 **“撤消事务”**。  
  
7.  在确认对话框中，单击 **“确定”**。 添加新事务，在 **“新值”** 列中显示 **“活动”** 。  
  
## 另请参阅  
 [删除成员或集合 (Master Data Services)](../master-data-services/delete-a-member-or-collection-master-data-services.md)   
 [成员 (Master Data Services)](../master-data-services/members-master-data-services.md)   
 [集合 (Master Data Services)](../master-data-services/collections-master-data-services.md)  
  
  