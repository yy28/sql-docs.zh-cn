---
title: "使用多维数据 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6e14c59fd0620129486408d33339e80624743f02
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="working-with-multidimensional-data"></a>使用多维数据
A*单元集*是对多维数据进行查询的结果。 它包含的轴，通常不超过四个轴，通常只有两个或三个集合。 *轴*是用于查找或筛选多维数据集中的特定值的一个或多个维度中的成员集合。  
  
 A*位置*是一个点沿 x 轴。 对于包含对单个维度的轴，这些位置是维度成员的子集。 如果一个轴包含多个维度，则每个位置是一个复合实体，它具有* n *部件 where * n *是沿该轴方向的维度数。 位置的每个部分是一个构成维度中的成员。  
  
 例如，如果从包含销售数据多维数据集 Geography 和产品维度的方向沿 x 轴的单元集，此轴的位置可能包含成员"USA"和"计算机。 在此示例中，确定沿 x 轴的位置需要每个维度中的成员的方向的轴平行。  
  
 A*单元格*是定位轴坐标的交叉点处的对象。 每个单元格中具有与其相关联，包括带格式的字符串 （单元数据可显示形式） 和单元格序号值数据本身的信息的多个部分。 （每个单元格是中的单元集的唯一序号值。 单元格集中的第一个单元的序号值为零，而包含八列是单元集的第二个行中最左侧单元格将具有八个的序号值。）  
  
 例如，多维数据集具有以下六个维度 (请注意此多维数据集架构给出的示例会稍有不同[概述多维架构和数据](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   销售人员  
  
-   Geography （自然层次结构）-洲、 国家/地区、 州等  
  
-   季度-季度，月天数  
  
-   Years  
  
-   度量值-销售，PercentChange，BudgetedSales  
  
-   Products  
  
 以下单元集的所有产品的 1991年表示销售：  
  
> [!NOTE]
>  在示例中的单元值可以看作是其中的第一个数字表示 x 轴位置，第二个数字的 y 轴位置的轴位置序号的有序对。  
  
 此单元集的特征如下所示：  
  
-   轴维度： 季度，销售人员，Geography  
  
-   筛选维度： 度量值，年，产品  
  
-   两个轴: （x 或轴 0） 的列和行 （y 或轴 1）  
  
-   x 轴： 两个嵌套的维度，销售人员和 Geography  
  
-   y 轴： 季度维度  
  
 X 轴具有两个嵌套的维度： 销售人员和 Geography。 从地理位置，选择四个成员： 西雅图、 波士顿，美国南部和日本。 从销售人员选择两个成员： 情人和 Nash。 这会生成总数 (8 = 4 * 2) 此轴上的 8 个位置。  
  
 每个坐标表示为具有两个成员的位置 — 一个来自销售人员维度，另一个来自 Geography 维度：  
  
```  
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 轴具有只有一个维度，包含以下八个位置：  
  
```  
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 单元集、 单元格、 轴和位置都表示 ADO MD 中由相应对象：[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)，[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，和[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多维） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多维架构和数据概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
