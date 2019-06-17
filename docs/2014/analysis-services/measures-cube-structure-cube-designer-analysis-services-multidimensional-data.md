---
title: 度量值 （多维数据集结构选项卡，多维数据集设计器） (Analysis Services-多维数据) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.cubebuilder.measurespane.f1
ms.assetid: be70f63b-58f2-4eff-81bc-c86d8229e617
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cbd64cd4eb3ca686fdbdd1a59c9e84fa387e6a7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077915"
---
# <a name="measures-cube-structure-tab-cube-designer-analysis-services---multidimensional-data"></a>度量值（“多维数据集结构”选项卡，多维数据集设计器）（Analysis Services - 多维数据）
  可以使用 **“度量值”** 窗格，操作多维数据集设计器中的 **“多维数据集结构”** 选项卡上的度量值组和成员。  
  
## <a name="options"></a>选项  
 “度量值”  
 根据所选视图显示多维数据集中包含的度量值组和度量值：  
  
 树  
 显示度量值组的树视图，度量值显示为子节点。  
  
 展开度量值组可以查看度量值。 单击所选度量值组或度量值可以分别重命名度量值组或度量值。  
  
 Grid  
 显示度量值网格以及最常访问的度量值属性。 单击 **“添加新度量值”** 可显示 **“新建度量值”** 对话框，向网格中添加新的度量值。  
  
 该网格包含以下列：  
  
 度量值  
 输入度量值的名称。  
  
 度量值组  
 显示包含该度量值的度量值组。  
  
 数据类型  
 选择度量值的数据类型。  
  
 聚合  
 选择度量值的聚合函数。  
  
## <a name="context-menu"></a>上下文菜单  
 右键单击“度量值”  窗格后，可以从所显示的上下文菜单中访问以下选项：  
  
 **新的度量值**  
 选择此选项可显示“新建度量值”对话框，以便向“度量值”窗格中当前所选的度量值组添加新度量值   。  
  
 **新建度量值组**  
 选择此选项可显示“新建度量值组”对话框，以便向“度量值”窗格中添加新度量值组   。  
  
 **度量值显示方式**  
 选择此选项可循环显示以下选项，或选择其中任一个选项以更改“度量值”  窗格的视图：  
  
|Option|定义|  
|------------|----------------|  
|**树**|在树视图中显示度量值组和度量值。|  
|**网格**|在网格中显示度量值组和度量值。|  
  
 **重命名**  
 选择此选项可重命名所选度量值组或度量值。  
  
 **删除**  
 选择此选项可显示“删除对象”对话框，以便删除“度量值”窗格中的所选对象   。  
  
 **上移**  
 选择此选项可将所选度量值组或度量值上移一个位置。  
  
> [!NOTE]  
>  如果无法向上移动所选项，将禁用此选项。  
  
 **“下移”**  
 选择此选项可将所选度量值组或度量值下移一个位置。  
  
> [!NOTE]  
>  如果无法向下移动所选项，将禁用此选项。  
  
 **新建链接的对象**  
 单击此项可显示 **链接对象向导** ，链接来自其他多维数据集的度量值组和维度，并向所选多维数据集导入操作、KPI 和计算。  
  
 **属性**  
 选择此选项可以为所选度量值组或度量值显示 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]“属性”  窗口。  
  
## <a name="see-also"></a>请参阅  
 [配置度量值属性](multidimensional-models/configure-measure-properties.md)   
 [度量值和度量值组](multidimensional-models/measures-and-measure-groups.md)  
  
  
