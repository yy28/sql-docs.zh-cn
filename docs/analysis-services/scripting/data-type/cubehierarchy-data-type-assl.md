---
title: "CubeHierarchy 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CubeHierarchy Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: CubeHierarchy
helpviewer_keywords: CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: "44"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7b69a18093cd54d21e2cb0e6ad557ff89f28cf35
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="cubehierarchy-data-type-assl"></a>CubeHierarchy 数据类型 (ASSL)
  定义一个基元数据类型，表示有关的信息[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)中的元素[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)，[启用](../../../analysis-services/scripting/properties/enabled-element-assl.md)， [HierarchyID](../../../analysis-services/scripting/properties/hierarchyid-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)， [OptimizedState](../../../analysis-services/scripting/properties/optimizedstate-element-assl.md)，[可见](../../../analysis-services/scripting/properties/visible-element-assl.md)|  
|派生元素|[层次结构](../../../analysis-services/scripting/objects/hierarchy-element-assl.md)([层次结构](../../../analysis-services/scripting/collections/hierarchies-element-assl.md)集合[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>注释  
 此数据类型没有任何限制，可在任何部署模式下使用：0 - 多维和数据挖掘；1 - SharePoint；2 - 表格。  
  
 SQL Server 2016 Analysis Services 及更高版本，*已启用*属性不能设置为**False**为*CubeHierarchy*。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeHierarchy>。  
  
## <a name="see-also"></a>另请参阅  
 [发现方法 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-methods-discover.md)   
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
