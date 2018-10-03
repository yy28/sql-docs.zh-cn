---
title: NamingTemplate 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- NamingTemplate Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NamingTemplate
helpviewer_keywords:
- NamingTemplate element
ms.assetid: d68d765c-f012-40c1-acd4-32741ee2eadf
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2b1a167ffc7418d69b28e8436bb67238acc3284b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106307"
---
# <a name="namingtemplate-element-assl"></a>NamingTemplate 元素 (ASSL)
  定义如何从构造的父子层次结构中命名级别[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)父元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
      <NamingTemplate>...</NamingTemplate>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 值`NamingTemplate`元素仅供父属性 (换而言之，值[用法](usage-element-dimensionattribute-assl.md)元素的`DimensionAttribute`父元素设置为*父*)。  
  
 当使用父属性构造层次结构时，该层次结构的级别由父属性包含的成员之间的父子关系确定。 因此，与其他维度不同级别的名称不能绘制从层次结构使用的属性名称。  
  
 相反，命名模板用于生成父子层次结构的级别名称。 在父属性中定义的 `NamingTemplate` 元素包含用于定义级别名称的字符串表达式。 有两种方法可以定义父属性的命名模板。 您可以设计一种命名模式，也可以指定名称列表。  
  
 命名模式包含一个星号 (`*`) 作为计数器占位字符，该计数器会递增并插入到每个更深的新级别的名称中。 例如，如果未定义“（全部）”级别，则使用 `Level *` 将得到级别名称 `Level 01`、`Level 02`、`Level 03` 等。 如果命名模式不包含占位字符，则它本身将作为第一个名称，后续的级别名称在此名称末尾加一个空格和一个数字。 例如，使用 `Level` 将得到级别名称 `Level`、`Level 01`、`Level 02` 等。  
  
 若要使用一组特定名称进行命名，`NamingTemplate` 元素的值应设置为以分号分隔的级别名称列表。 列表中的每个名称都用于后续级别名称。 如果级别数超出了列表中的名称数，则列表中的最后一个名称将用作任何其他级别名称的模板，如前所述，在该名称后加一个空格和一个序号。 例如，使用 `Division;Group;Unit` 将得到级别名称 `Division`、`Group`、`Unit`、`Unit 01`、`Unit 02` 等。 相比之下，使用 `Division;Group;Unit *` 则得到级别名称 `Division`、`Group`、`Unit 03`、`Unit 04` 等。  
  
 列表中的每个名称都视为一个模板，以确保级别名称的唯一性。 例如，使用 `Manager;Team Lead;Manager;Team Lead;Worker *` 将得到级别名称 `Manager`、`Team Lead`、`Manager 01`、`Team Lead 01`、`Worker 05`、`Worker 06`。  
  
 使用两个星号 （*） 来包含星号 (\*) 字符作为命名模板的一部分的级别名称中。  
  
 父级对应的元素`NamingTemplate`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [NamingTemplateTranslations 元素&#40;ASSL&#41;](../collections/translations-element-assl.md)   
 [DimensionAttribute 数据类型&#40;ASSL&#41;](../data-type/dimensionattribute-data-type-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
