---
title: "\"创建或编辑关系\" 对话框（Analysis Services 多维数据） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createrelationship.f1
helpviewer_keywords:
- Create Relationship dialog box
ms.assetid: da3c7074-623e-4ddf-a707-d3276a47cf1c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: de19592ec5a94e99cc87c40dac476e75546c7968
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086779"
---
# <a name="create-or-edit-relationship-dialog-box-analysis-services---multidimensional-data"></a>“创建或编辑关系”对话框（Analysis Services - 多维数据）
  可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的“创建/编辑关系”**** 对话框，定义或修改数据源视图中的关系。 通过执行以下操作之一，可以显示“创建/编辑关系”对话框****：  
  
-   在 **数据源视图设计器** 的 **“工具栏”** 窗格中，单击 **“新建关系”**。  
  
-   右键单击**数据源视图设计器**的“表”**** 窗格或“关系图”**** 窗格中的表，再选择“新建关系”****。  
  
-   右键单击**数据源视图设计器**的“关系图”**** 窗格中的关系，再选择“编辑关系”****。  
  
> [!NOTE]  
>   可以在 **数据源视图设计器** 中创建基础数据源中不存在的关系，并从基础数据源中的现有外键关系中删除通过 **数据源视图设计器** 创建的关系。  
  
## <a name="options"></a>选项  
 **源(外键)表**  
 选择包含对目标表中一个或多个列的引用的表或命名查询。  
  
 **目标(主键)表**  
 选择包含源表所引用的一个或多个列的表。 对于自联接，请选择在“源(外键)表”**** 中选择的同一个表。  
  
 **源列**  
 选择引用目标表中的列的列。  
  
 **目标列**  
 选择被源表中的列引用的列。  
  
 **反向**  
 单击此项可以使关系方向变为相反方向。  
  
 **说明**  
 键入关系的说明（可选）。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [数据源视图设计器（Analysis Services - 多维数据）](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
