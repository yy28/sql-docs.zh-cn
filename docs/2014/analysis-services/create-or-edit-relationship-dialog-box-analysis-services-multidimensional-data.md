---
title: 创建或编辑关系对话框 (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createrelationship.f1
helpviewer_keywords:
- Create Relationship dialog box
ms.assetid: da3c7074-623e-4ddf-a707-d3276a47cf1c
caps.latest.revision: 19
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 152f9cb38adcad9a90a393150216fea0f10ecd55
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37167638"
---
# <a name="create-or-edit-relationship-dialog-box-analysis-services---multidimensional-data"></a>“创建或编辑关系”对话框（Analysis Services - 多维数据）
  可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中的“创建/编辑关系”对话框，定义或修改数据源视图中的关系。 通过执行以下操作之一，可以显示“创建/编辑关系”对话框：  
  
-   在 **数据源视图设计器** 的 **“工具栏”** 窗格中，单击 **“新建关系”**。  
  
-   右键单击**数据源视图设计器**的“表”窗格或“关系图”窗格中的表，再选择“新建关系”。  
  
-   右键单击**数据源视图设计器**的“关系图”窗格中的关系，再选择“编辑关系”。  
  
> [!NOTE]  
>  可以在**数据源视图设计器**中创建基础数据源中不存在的关系，并从基础数据源中的现有外键关系中删除通过**数据源视图设计器**创建的关系。  
  
## <a name="options"></a>“常规”  
 **源 （外键） 表**  
 选择包含对目标表中一个或多个列的引用的表或命名查询。  
  
 **目标 （主键） 表**  
 选择包含源表所引用的一个或多个列的表。 对于自联接，请选择在“源(外键)表”中选择的同一个表。  
  
 **源列**  
 选择引用目标表中的列的列。  
  
 **目标列**  
 选择被源表中的列引用的列。  
  
 **反向**  
 单击此项可以使关系方向变为相反方向。  
  
 **Description**  
 键入关系的说明（可选）。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 设计器和对话框&#40;多维数据&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [数据源视图设计器&#40;Analysis Services-多维数据&#41;](data-source-view-designer-analysis-services-multidimensional-data.md)  
  
  
