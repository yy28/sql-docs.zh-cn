---
title: 多维模型中的透视 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- default members
- hiding objects from perspective
- renaming perspectives
- attributes [Analysis Services], default members
- removing perspectives
- perspectives [Analysis Services]
- names [Analysis Services], perspectives
- cubes [Analysis Services], perspectives
- deleting perspectives
ms.assetid: 5a3d6577-6833-4c24-820c-b65bb856157b
caps.latest.revision: 27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 65bda021dbb7f52b9039255226221b3718b61d8b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37188924"
---
# <a name="perspectives-in-multidimensional-models"></a>多维模型中的透视
  透视是为特定应用程序或用户组创建的多维数据集的子集。 多维数据集本身是一个默认的透视。 透视针对客户端显示为一个多维数据集。 当用户查看透视时，该透视看上去像另一个多维数据集。 在透视中通过写回对多维数据集数据所做的任何更改也会作用于原始多维数据集。 有关 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中视图的详细信息，请参阅 [透视图](../multidimensional-models-olap-logical-cube-objects/perspectives.md)。  
  
 使用多维数据集设计器的 **“透视”** 选项卡，可以创建或修改多维数据集中的透视。 **“透视”** 选项卡的第一列是 **“多维数据集对象”** 列，该列列出多维数据集中的所有对象。 这对应于多维数据集的默认透视，该透视是多维数据集本身。  
  
## <a name="creating-or-deleting-perspectives"></a>创建或删除透视  
 您可以通过在 **“多维数据集”** 菜单中单击 **“新建透视”** ，将某个透视添加到 **“透视”** 选项卡中。 还可以单击工具栏上的“新建透视图”按钮，或者右键单击窗格中的任意位置，再单击快捷菜单中的“新建透视图”。 您可以向多维数据集中添加任意数量的透视。  
  
 若要删除透视，请首先单击要删除的透视的列中的任意单元。 然后在 **“多维数据集”** 菜单中，单击 **“删除透视”**。 还可以单击工具栏上的“删除透视图”按钮，或者右键单击要删除的透视图中的任意单元格，再单击快捷菜单中的“删除透视图”。  
  
## <a name="renaming-perspectives"></a>重命名透视  
 每个透视的第一行都显示该透视的名称。 当您创建透视时，最初的名称便是“Perspective”（如果已经存在名为“Perspective”的透视，则在该名称后面紧跟以 1 开始的序号）。 您可以单击名称对其进行编辑。  
  
## <a name="hiding-objects-from-a-perspective"></a>对透视隐藏对象  
 若要对透视隐藏对象，请清除与透视列中的对象对应的行中的复选框。 可以对透视隐藏的多维数据集对象包括：  
  
-   度量值组  
  
-   度量值组  
  
-   维度  
  
-   层次结构  
  
-   命名集  
  
-   KPI  
  
-   操作  
  
-   计算成员  
  
 若要查看任意对象，请展开“多维数据集对象”下任意对象类型的类别（“度量值组”、“维度”、“KPI”、“计算”或“操作”）。 若要查看维度中的层次结构或属性，请首先展开维度，然后展开 **“层次结构”** 或 **“属性”** 行。 若要查看度量值组中的度量值，请展开度量值组。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的多维数据集](cubes-in-multidimensional-models.md)  
  
  
