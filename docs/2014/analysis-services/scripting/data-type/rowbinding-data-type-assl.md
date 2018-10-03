---
title: RowBinding 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- RowBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RowBinding
helpviewer_keywords:
- RowBinding data type
ms.assetid: 5a49a6e3-25f3-43c8-8529-bcf245b02415
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9fb15b72b3031b62136f65b175cb0ded8c3297a9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203217"
---
# <a name="rowbinding-data-type-assl"></a>RowBinding 数据类型 (ASSL)
  定义一个派生的数据类型，表示的绑定中的表的行[DataSourceView](../objects/datasourceview-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RowBinding>  
   <!-- The following elements extend Binding -->  
   <TableID>...</TableID>  
</RowBinding>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[绑定](binding-data-type-assl.md)|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[TableID](../properties/id-element-assl.md)|  
|派生元素|请参阅[绑定](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>备注  
 有关详细信息`Binding`类型，包括 Analysis Services 脚本语言 (ASSL) 对象的表`Binding`类型和继承层次结构`Binding`类型，请参阅[绑定数据类型&#40;ASSL&#41;](binding-data-type-assl.md).  
  
 有关 ASSL 中数据绑定的概述，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.RowBinding>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
