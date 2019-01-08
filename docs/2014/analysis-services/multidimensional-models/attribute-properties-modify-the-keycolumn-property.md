---
title: 修改特性的 KeyColumn 属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- binding attributes [Analysis Services]
- attributes [Analysis Services], binding
- key columns [Analysis Services]
ms.assetid: a2643be4-8123-4cc3-baf9-e5ec54a1669d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92624d18c0e8aae6a549f0769277e5fd4fdd0c34
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524363"
---
# <a name="modify-the-keycolumn-property-of-an-attribute"></a>修改某个特性的 KeyColumn 属性
  可以修改特性的 **KeyColumns** 属性。 例如，您可能需要指定组合键以作为该特性的键，而不是指定单个键。  
  
### <a name="to-modify-the-keycolumns-property-of-an-attribute"></a>修改某个特性的 KeyColumns 属性  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，打开要修改其中 **KeyColumns** 属性的项目。  
  
2.  通过执行下列过程之一打开维度设计器：  
  
    -   在**解决方案资源管理器**中，右键单击“维度”文件夹中的维度，然后单击“打开”或“视图设计器”。  
  
         -或-  
  
    -   在多维数据集设计器上**多维数据集结构**选项卡上，展开中的多维数据集维度**维度**窗格，然后单击**编辑\<维度 >**。  
  
3.  在 **“维度结构”** 选项卡的 **“属性”** 窗格中，单击要修改其 **KeyColumns** 属性的特性。  
  
4.  在 **“属性”** 窗口中，单击 **KeyColumns** 属性的值。  
  
5.  单击在属性框的值单元中出现的浏览按钮 **(...)** 。  
  
     **“键列”** 对话框将打开。  
  
6.  若要删除现有键列，请在“键列”列表中选择相应的列，然后单击“\<”按钮。  
  
7.  若要添加键列，请在“可用列”列表中选择相应的列，然后单击“>”按钮。  
  
    > [!NOTE]  
    >  如果定义多个键列，则这些列在 **“键列”** 列表中的排序将影响键列的显示顺序。 例如，月特性有两个键列：月和年。 如果列表中年列显示在月列前，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将先按年进行排序，再按月进行排序。 如果月列显示在年列前，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将先按月进行排序，再按年进行排序。  
  
8.  若要更改键列的顺序，请选择一列，然后单击 **“向上”** 或 **“向下”** 按钮。  
  
## <a name="see-also"></a>请参阅  
 [维度特性属性参考](dimension-attribute-properties-reference.md)  
  
  
