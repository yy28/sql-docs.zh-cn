---
title: 使用多维数据 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional data [ADO]
ms.assetid: 84387746-aa3e-44fd-ad6c-a8214a6966dc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cb1f29a3037cafdddc14973f77d7bb3d8c52f296
ms.sourcegitcommit: 96b2355d54dfad259826e88bdff91cc9344e16f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2018
ms.locfileid: "51350264"
---
# <a name="working-with-multidimensional-data"></a>使用多维数据
一个*单元集*是多维数据的查询的结果。 它包含的轴，通常不超过四个轴，通常只有两个或三个集合。 *轴*是来自一个或多个维度的成员的集合，用于查找或筛选多维数据集中的特定值。  
  
 一个*位置*是沿某个轴的点。 包含单个维度的轴，这些位置是维度成员的子集。 如果一个轴包含多个维度，则每个位置是一个复合实体，它具有*n*部件 where *n*是沿该轴方向的维度数。 位置的每个部分是一个构成维度中的成员。  
  
 例如，如果从包含销售数据的多维数据集地域和产品维度面向沿 x 轴的单元集，沿此轴的位置可能包含的成员"USA"和"计算机。 在此示例中，确定沿 x 轴的位置需要，沿轴方向，从每个维度的成员。  
  
 一个*单元格*是定位轴坐标相交处的对象。 每个单元格有多个部分的信息包括数据本身、 格式化的字符串 （单元格数据的可显示形式） 和单元格序号值与其关联。 （每个单元格是一个唯一的序号值单元格集中。 中的单元集的第一个单元格的序数值为零，而第二行的单元集内包含八列中的最左侧单元格将具有的序号值为 8。）  
  
 例如，多维数据集具有以下六个维度 (请注意此多维数据集架构给出的示例会稍有不同[概述的多维架构和数据](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)):  
  
-   销售人员  
  
-   Geography （自然层次结构） — 大洲、 国家/地区、 州等  
  
-   季度-季度、 月、 天  
  
-   Years  
  
-   度量值-销售，PercentChange，BudgetedSales  
  
-   Products  
  
 下面的单元集表示 1991 的所有产品的销售额：  
  
> [!NOTE]
>  在示例中的单元值可以视为轴位置序号其中第一个数字表示 x 轴位置，第二个数字 y 轴位置的有序对。  
  
 此单元集的特征如下所示：  
  
-   轴维度： 季度，销售人员，Geography  
  
-   筛选维度： 度量值，年中，产品  
  
-   两个轴: （x 或轴 0） 的列和行 （y 或轴 1）  
  
-   x 轴： 两个嵌套的维度，销售人员和地理位置  
  
-   y 轴： 季度维度  
  
 X 轴包含两个嵌套的维度： 销售人员和地理位置。 从地理位置，选择四个成员： 西雅图，波士顿，美国南部和日本。 两个成员从销售人员选择： 情人和 Nash。 这会生成总共八位 (8 = 4 * 2) 此轴上。  
  
 每个坐标表示为具有两个成员的位置 — 一个来自销售人员维度，地域维度中的另一个：  
  
```console
(Valentine, Seattle), (Valentine, Boston), (Valentine, USA_North),  
(Valentine, Japan), (Nash, Seattle), (Nash, Boston), (Nash, USA_North),  
(Nash, Japan)  
```  
  
 Y 轴具有只有一个维度，其中包含以下 8 个位置：  
  
```console
Jan, Feb, Mar, Qtr2, Qtr3, Oct, Nov, Dec  
```  
  
 单元集、 单元格、 轴和位置都表示 ADO MD 中的相应对象：[单元集](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)，[单元格](../../../ado/reference/ado-md-api/cell-object-ado-md.md)，[轴](../../../ado/reference/ado-md-api/axis-object-ado-md.md)，和[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md).  
  
## <a name="see-also"></a>请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多维） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [多维架构和数据的概述](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [使用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)
