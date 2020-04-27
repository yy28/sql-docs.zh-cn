---
title: "\"度量值组绑定\" 对话框（Analysis Services 多维数据） |Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.measuregroupbindings.f1
helpviewer_keywords:
- Measure Group Bindings dialog box
ms.assetid: ed642780-5350-438e-af73-b9ceab3f876d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d3d04692ac6576e76d2b630fb5cacb4f57db959
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077860"
---
# <a name="measure-group-bindings-dialog-box-analysis-services---multidimensional-data"></a>“度量值组绑定”对话框（Analysis Services - 多维数据）
  对于常规维度关系，可以使用“度量值组绑定”对话框创建和修改多维数据集维度中的非粒度属性与度量值组中的列之间的直接关系，并使用“定义关系”对话框为多维数据集维度中的所有属性指定空值处理选项。********  
  
## <a name="options"></a>选项  
 **度量值组表**  
 显示所选度量值组的事实数据表的名称。  
  
 **特性**  
 显示属性和维度表的网格。 选择一个属性可以在 **“关系”** 中为所选属性创建或修改其属性。 该网格包含以下列：  
  
|选项|定义|  
|------------|----------------|  
|**属性名称**|显示属性的名称。|  
|**维度表**|显示属性所基于的维度表的名称。|  
  
 **关系**  
 显示所选属性的维度表列与所选度量值组的事实数据表列之间的关系网格，并显示关系的空值处理选项。 该网格包含以下列：  
  
|选项|定义|  
|------------|----------------|  
|**维度列**|显示在 **“属性”** 中选择的属性所基于的维度表中的列。|  
|**度量值组列**|选择 **“从维度继承”** 可以使用从维度继承的度量值组关系，或者从度量值组所基于的事实数据表选择列，以显式定义关系。|  
|**空值处理**|为属性选择空值处理选项。 有关空值处理选项的详细信息，请参阅 [NullProcessing 元素 (ASSL)](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl)。|  
  
## <a name="see-also"></a>另请参阅  
 ["定义关系" 对话框 &#40;Analysis Services 多维数据&#41;](define-relationship-dialog-box-analysis-services-multidimensional-data.md)   
 [&#40;多维数据的 Analysis Services 设计器和对话框&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
