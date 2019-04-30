---
title: 多维架构和数据的概述 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- multidimensional schemas and data
ms.assetid: ce37fa06-c581-4d80-9a9b-c3aa66408909
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f06f62768637ebb48ffa6e1cfd2560ff3b53c383
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63194913"
---
# <a name="overview-of-multidimensional-schemas-and-data"></a>多维架构和数据的概述
## <a name="understanding-multidimensional-schemas"></a>了解多维架构  
 ADO MD 中的中央元数据对象是*多维数据集*，其中包含结构化的一组相关的维度、 层次结构、 级别和成员。  
  
 一个*维度*是一个独立的多维数据库，派生自您的业务实体中的数据类别。 维度通常包含要用作查询条件的数据库的度量值的项。  
  
 一个*层次结构*是聚合的维度的路径。 维度可能具有多个级别的粒度，具有父-子关系。 层次结构定义如何关联这些级别。  
  
 一个*级别*是聚合的层次结构中的步骤。 对于具有多个层的维度，每一层是信息的一个级别。  
  
 一个*成员*是维度中的数据项。 通常情况下，创建一个标题或描述数据库使用的成员的度量值。  
  
 多维数据集表示通过[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) ADO MD.中的对象 其相应的 ADO MD 对象还表示维度、 层次结构、 级别和成员：[维度](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)，[层次结构](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)，[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)，并且[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)。  
  
### <a name="dimensions"></a>维度  
 多维数据集维度取决于你的业务实体和要在数据库中建模的数据类型。 通常情况下，每个维度是一个独立的入口点或机制，用于选择数据。  
  
 例如，包含销售数据的多维数据集具有以下五个维度：销售人员、 地理位置、 时间、 产品和度量值。 度量值维度包含实际的销售数据值，而其他维度表示方式进行分类和分组的销售数据值。  
  
 地域维度具有以下一组成员：  
  
```console
{All, North America, Europe, Canada, USA, UK, Germany, Canada-West,  
Canada-East, USA-NW, USA-SW, USA-NE, USA-SE, England, Scotland,   
Wales,Ireland, Germany-North, Germany-South, Ottawa, Toronto,   
Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston,   
Shreveport, Miami, Boston, New York, London, Dover, Glasgow,   
Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin,   
Hamburg, Munich, Stuttgart}  
```  
  
### <a name="hierarchies"></a>层次结构  
 层次结构定义中的维度级别可以"汇总"或分组的方式。 维度可以具有多个层次结构。 地域维度中存在自然层次结构：  
  
### <a name="levels"></a>Levels  
 在上图中所示示例 Geography 维度中，每个框表示层次结构中的级别。  
  
 每个级别都有一组的成员，按如下所示：  
  
-   世界 `= {All}`  
  
-   大洲 `= {North America, Europe}`  
  
-   国家/地区 `= {Canada, USA, UK, Germany}`  
  
-   区域 `= {Canada-East, Canada-West, USA-NE, USA-NW, USA-SE, USA-SW, England, Ireland, Scotland, Wales, Germany-North, Germany-South}`  
  
-   城市 `= {Ottawa, Toronto, Vancouver, Calgary, Seattle, Boise, Los Angeles, Houston, Shreveport, Miami, Boston, New York, London, Dover, Glasgow, Edinburgh, Cardiff, Pembroke, Belfast, Derry, Berlin, Hamburg, Munich, Stuttgart}`  
  
### <a name="members"></a>成员  
 在层次结构的叶级别的成员具有任何子级，并在根级别的成员具有没有父级。 所有其他成员有至少一个父类和至少一个子级。 例如，地域维度中的层次结构树的部分遍历生成以下父-子关系：  
  
-   `{All} (parent of) {Europe, North America}`  
  
-   `{North America} (parent of) {Canada, USA}`  
  
-   `{USA} (parent of) {USA-NE, USA-NW, USA-SE, USA-SW}`  
  
-   `{USA-NW} (parent of) {Boise, Seattle}`  
  
 可以按每个维度的一个或多个层次结构合并成员。 时间维度，请考虑在有两种方法来从天级别为 Year 级别汇总：  
  
 此示例还演示了另一个特征：年周层次结构的一周级别的某些成员不显示在年季度层次结构的任何级别。 因此，层次结构不需要包括维度的所有成员。  
  
## <a name="see-also"></a>请参阅  
 [ADO MD 对象模型](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [ADO （多维） (ADO MD)](../../../ado/guide/multidimensional/ado-multidimensional-ado-md.md)   
 [使用 ADO MD 进行编程](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [使用 ADO 与 ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [使用多维数据](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
