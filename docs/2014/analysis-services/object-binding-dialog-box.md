---
title: "\"对象绑定\" 对话框 |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql.asvs.dimensiondesigner.dbv.objectbinding.f1
helpviewer_keywords:
- Object Binding dialog box
ms.assetid: 2bb5ad7c-2962-4559-8c95-cf7148bd2e72
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9cc86a5712dae9c231fa6e03d86a82d7dc172a75
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072189"
---
# <a name="object-binding-dialog-box"></a>“对象绑定”对话框
  使用 **中的** “对象绑定” [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 对话框，可以定义 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的属性与数据源视图中的表或列之间的绑定。 在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 的“属性”**** 窗口中，通过从 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象的下列属性值的下拉列表中选择“(新建)”****，可以显示“对象绑定”**** 对话框：  
  
-   NameColumn  
  
-   ValueColumn  
  
-   CustomRollupColumn  
  
-   CustomRollupPropertiesColumn  
  
-   UnaryOperatorColumn  
  
## <a name="options"></a>选项  
 **绑定类型**  
 选择要为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象使用的绑定。 可以使用以下类型的绑定：  
  
 列绑定  
 将对象绑定到数据源视图中的现有表和列。  
  
 生成列  
 指示将在数据源视图中定义新列，然后将列绑定与其相关联。  
  
> [!NOTE]  
>  如果选中此选项，则必须在部署 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象之前运行“架构生成向导”****。  
  
 行绑定  
 将对象绑定到事实数据表中的行，用于支持基于事实数据表中已处理行数的计数度量值。  
  
 **源表**  
 显示数据源视图中与 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 对象关联的表的列表。  
  
 **源列**  
 显示在“源表”**** 中选择的表中列的列表。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
