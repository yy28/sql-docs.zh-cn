---
title: "Filter Data before Exporting (MDS Add-in for Excel) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "master-data-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e30eae0-776b-4a09-aac3-0c0249d92ca5
caps.latest.revision: 10
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 10
---
# Filter Data before Exporting (MDS Add-in for Excel)
  在 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], ，当你想要限制的大小或将导出到 Excel 的数据的范围筛选数据。  
  
## 先决条件  
 若要执行此过程：  
  
-    您必须有权访问“资源管理器”功能区域。  
  
### 若要在导出之前筛选数据  
  
1.  打开 Excel，在 **“主数据”** 选项卡上连接到 MDS 存储库。 有关详细信息，请参阅 [连接到 MDS 存储库 & #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)。  
  
2.  在 **“主数据资源管理器”** 窗格中，选择所需模型和版本。 随之填充实体列表。  
  
    -   如果 **“主数据资源管理器”** 窗格不可见，请在 **“连接并加载”** 组中，单击 **“显示资源管理器”**。  
  
    -   如果 **主数据资源管理器** 窗格被禁用，这是因为现有的表已包含 MDS 管理的数据。 若要启用该窗格，请打开一个新工作表。  
  
3.  在 **“主数据资源管理器”** 窗格的实体列表中，单击要筛选的实体。  
  
4.  在功能区上的 **“连接并加载”** 组中，单击 **“筛选器”**。  
  
5.  完成 **筛选器** 对话框中通过选择要显示的属性 （列），这些列的顺序设置，如果需要请筛选数据，以便返回更少的行。 查看 **“摘要”** 窗格了解将返回的数据量。 有关详细信息，请参阅 [筛选器对话框中 & #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)。  
  
6.  单击 **“加载数据”**。 将使用 MDS 管理的数据填充工作表。  
  
    > [!NOTE]  
    >  -   只有前一百万个成员才能加载到 Excel 中。  
    > -   在作为约束列表（基于域的属性）的列中，默认情况下只加载前 25000 个值。  
  
## 后续步骤  
 [将数据从 Excel 导入到 Master Data Services & #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)  
  
## 另请参阅  
 [概述︰ 将数据导出到 Excel & #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)   
 [筛选器对话框中 & #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/filter-dialog-box-mds-add-in-for-excel.md)   
 [重新排序的列和 #40;MDS add-in for Excel 和 #41;](../../master-data-services/microsoft-excel-add-in/reorder-columns-mds-add-in-for-excel.md)  
  
  