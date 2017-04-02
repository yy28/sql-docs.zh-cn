---
title: "转换数据源（报表生成器和 SSRS） | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "数据源 [Reporting Services], 嵌入"
  - "数据源 [Reporting Services], 共享"
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
caps.latest.revision: 16
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 16
---
# 转换数据源（报表生成器和 SSRS）
  “报表数据”窗格中的每个数据源都是嵌入且特定于报表的，或者是共享的。 在报表生成器中，共享数据源将指向报表服务器或 SharePoint 站点上的已发布共享数据源。 在报表设计器中，共享数据源将指向解决方案资源管理器中 **“共享数据源”** 文件夹下的某一共享数据源。  
  
 有关嵌入数据源与共享数据源之间的差异的详细信息，请参阅[嵌入和共享的数据连接或数据源（报表生成器和 SSRS）](../Topic/Embedded%20and%20Shared%20Data%20Connections%20or%20Data%20Sources%20\(Report%20Builder%20and%20SSRS\).md)。  
  
 有关如何创建共享数据源的详细信息，请参阅[创建嵌入或共享数据源 (SSRS)](../Topic/Create%20an%20Embedded%20or%20Shared%20Data%20Source%20\(SSRS\).md)。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 报表设计器  
  
#### 将嵌入数据源转换为共享数据源  
  
-   在“报表数据”窗格中，右键单击数据源，然后单击“转换为共享数据源”。  
  
    > [!NOTE]  
    >  如果“报表数据”窗格不可见，请单击 **“视图”** 菜单上的 **“报表数据”**。 如果“报表数据”窗格以浮动窗口形式打开，则请停靠该窗格。 有关详细信息，请参阅[在报表设计器中停靠“报表数据”窗格 (SSRS)](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md)。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。 在解决方案资源管理器中， **“共享数据源”** 文件夹中会出现一个同名的共享数据源。  
  
### 将共享数据源转换为嵌入数据源  
  
-   在“报表数据”窗格中，右键单击数据源，打开“数据源属性”对话框，然后单击“嵌入连接”。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
## 报表生成器  
  
#### 将嵌入数据源转换为共享数据源  
  
-   在“报表数据”窗格中，右键单击数据源以便打开“数据源属性”对话框，然后单击“嵌入连接”。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
#### 将共享数据源转换为嵌入数据源  
  
-   在“报表数据”窗格中，右键单击数据源，打开“数据源属性”对话框，然后单击“嵌入连接”。 输入必需的信息。  
  
     在“报表数据”窗格中，数据源图标将更改为共享数据源图标。  
  
## 另请参阅  
 [管理报表数据源](../../reporting-services/report-data/manage-report-data-sources.md)   
 [数据连接、数据源和连接字符串（报表生成器和 SSRS）](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  