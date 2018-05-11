---
title: 修改特性的 KeyColumn 属性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ed11e4655af481bf3ee9b3748110767fa2ad60b3
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="attribute-properties---modify-the-keycolumn-property"></a>特性属性-修改 KeyColumn 属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  可以修改特性的 **KeyColumns** 属性。 例如，您可能需要指定组合键以作为该特性的键，而不是指定单个键。  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>修改某个特性的 KeyColumns 属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要修改其中 **KeyColumns** 属性的项目。  
  
2.  通过执行下列过程之一打开维度设计器：  
  
    -   在**解决方案资源管理器**中，右键单击“维度”文件夹中的维度，然后单击“打开”或“视图设计器”。  
  
         — 或 —  
  
    -   在多维数据集设计器上**多维数据集结构**选项卡上，展开中的多维数据集维度**维度**窗格中，然后单击**编辑\<维度 >**。  
  
3.  在 **“维度结构”** 选项卡的 **“属性”** 窗格中，单击要修改其 **KeyColumns** 属性的特性。  
  
4.  在 **“属性”** 窗口中，单击 **KeyColumns** 属性的值。  
  
5.  单击在属性框的值单元中出现的浏览按钮 **(...)** 。  
  
     **“键列”** 对话框将打开。  
  
6.  若要删除现有键列，请在“键列”列表中选择相应的列，然后单击“\<”按钮。  
  
7.  若要添加键列，请在“可用列”列表中选择相应的列，然后单击“>”按钮。  
  
    > [!NOTE]  
    >  如果定义多个键列，则这些列在 **“键列”** 列表中的排序将影响键列的显示顺序。 例如，月特性有两个键列：月和年。 如果列表中年列显示在月列前，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将先按年进行排序，再按月进行排序。 如果月列显示在年列前，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将先按月进行排序，再按年进行排序。  
  
8.  若要更改键列的顺序，请选择一列，然后单击 **“向上”** 或 **“向下”** 按钮。  
  
## <a name="see-also"></a>另请参阅  
 [维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
