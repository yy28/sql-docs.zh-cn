---
title: "为多维数据的参数值显示隐藏的数据集（报表生成器和 SSRS） | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eb01c4ca-4fd6-4629-b595-f0d2565915df
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# 为多维数据的参数值显示隐藏的数据集（报表生成器和 SSRS）
  报表可能包括默认在“报表数据”窗格中不显示的自动生成的数据集（也称为隐藏数据集）。 这些数据集是用下列方法创建的：  
  
-   在用于多维数据库的某些查询设计器中，可以在查询窗格的筛选区域中指定要筛选的字段，并选择是否为筛选器创建查询参数。 如果选择参数选项，会自动创建报表数据集以便为报表参数提供有效的值。  
  
-   如果导入基于多维数据库的查询，则还可能将隐藏数据集包括在报表中。  
  
 无法通过向导使用隐藏数据集。  
  
 可以更改“报表数据”窗格中的视图以显示报表中的所有数据集。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### 显示隐藏数据集  
  
-   在“报表数据”窗格中，右键单击“数据集”文件夹，然后单击“显示隐藏数据集”。  
  
## 另请参阅  
 [查询设计器（报表生成器）](../Topic/Query%20Designers%20\(Report%20Builder\).md)   
 [Reporting Services 查询设计器](../Topic/Reporting%20Services%20Query%20Designers.md)   
 [报表的嵌入数据集和共享数据集（报表生成器和 SSRS）](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [报表数据集 (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)  
  
  