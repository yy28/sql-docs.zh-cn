---
title: CubeHierarchy 数据类型 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CubeHierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeHierarchy
helpviewer_keywords:
- CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 48176b4096b7fa7ba8e1847750410be0f65da552
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123493"
---
# <a name="cubehierarchy-data-type-assl"></a>CubeHierarchy 数据类型 (ASSL)
  定义一个基元数据类型，表示有关的信息[层次结构](../objects/hierarchy-element-assl.md)中的元素[多维数据集](../objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[批注](../collections/annotations-element-assl.md)，[启用](../properties/enabled-element-assl.md)， [HierarchyID](../properties/id-element-assl.md)，[名称](../properties/name-element-assl.md)， [OptimizedState](../properties/state-element-assl.md)，[可见](../properties/visible-element-assl.md)|  
|派生元素|[层次结构](../objects/hierarchy-element-assl.md)([层次结构](../collections/hierarchies-element-assl.md)集合[CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 此数据类型没有任何限制，可在任何部署模式下使用：0 - 多维和数据挖掘；1 - SharePoint；2 - 表格。  
  
 在[!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)]、*已启用*属性不能设置为`False`为*CubeHierarchy*。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeHierarchy>。  
  
## <a name="see-also"></a>请参阅  
 [发现方法&#40;XMLA&#41;](../../xmla/xml-elements-methods-discover.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  