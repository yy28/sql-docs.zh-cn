---
title: 多维架构和数据概述 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 304dd62f748fd58c314286ceedb6e2a5c22dd029
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多维架构和数据概述
## <a name="understanding-multidimensional-schemas"></a>了解多维架构  
 ADO MD 中的中央元数据对象*多维数据集*，它包括一组结构化的相关的维度、 层次结构、 级别和成员。  
  
 A*维度*是独立的多维数据库，派生自您的业务实体中的数据类别。 维度通常包含用于数据库的度量值的作为查询条件的项。  
  
 A*层次结构*是聚合的维度的路径。 维度可能具有多个级别的粒度，其具有父-子关系。 层次结构定义这些级别相关联的方式。  
  
 A*级别*是聚合层次结构中的步骤。 对于具有多个层的维度，每个层是信息的一个级别。  
  
 A*成员*是维度中的数据项。 通常情况下，你创建一个标题或描述使用成员的数据库的度量值。  
  
 多维数据集表示通过[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ADO MD.中的对象 维度、 层次结构、 级别和成员也表示由其相应的 ADO MD 对象：[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)，和[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)。  
  
### <a name="dimensions"></a>维度  
 多维数据集维度取决于你的业务实体和要在数据库中建模的数据类型。 通常情况下，每个维度是一个独立的入口点或机制，用于选择数据。  
  
 例如，多维数据集包含销售数据具有以下五个维度： 销售人员、 Geography、 时间、 产品和度量值。 度量值维度包含实际的销售数据值，而其他维度表示方式进行分类和分组的销售数据值。  
  
 Geography 维度具有以下一组成员：  
  
```  
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>层次结构  
 层次结构定义在其中一个维度的级别可以"汇总"或分组的方式。 维度可以具有多个层次结构。 Geography 维度中存在的自然层次结构：  
  
### <a name="levels"></a>Levels  
 在上一图中的示例 Geography 维度中，每个框表示层次结构中的级别。  
  
 每个级别具有一组的成员，如下所示：  
  
-   世界 `= {All}`  
  
-   洲和 `= {North America, Europe}`  
  
-   国家/地区 `= {Canada, USA, UK, Germany}`  
  
-   区域 `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   城市 `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>成员  
 叶级别的层次结构的成员具有没有子级，并且在根级别的成员具有没有父级。 所有其他成员有至少一个父类和至少一个子级。 例如，Geography 维度中的层次结构树的部分遍历产生以下的父-子关系：  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 每个维度的一个或多个层次结构，可以合并成员。 时间维度，请考虑其中有两种方法可以汇总到年级别从天级别：  
  
 此示例还演示了另一个特性： 年周层次结构的周级别的某些成员未出现在年季度层次结构的任何一级别。 因此，层次结构不需要包括维度的所有成员。  
  
## <a name="see-also"></a>另请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多维） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [使用 ADO MD 编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 的 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
