---
title: "Name 属性 (ADO MD) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Level::Name
- CubeDef::Name
- Member::Name
- Catalog::Name
- Dimension::Name
- Name
- Axis::Name
- Hierarchy::Name
helpviewer_keywords: Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e471f2ea21a72b6034fa522ced7681965b733d91
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="name-property-ado-md"></a>Name 属性 (ADO MD)
指示对象的名称。  
  
## <a name="return-values"></a>返回值  
 返回**字符串**和是只读的。  
  
## <a name="remarks"></a>Remarks  
 你可以检索**名称**按序号引用，此后可以按名称直接引用对象的对象属性。 例如，如果`cdf.CubeDefs(0).Name`产生"Bobs 视频存储"，您可以参考此[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)作为`cdf.CubeDefs("Bobs Video Store")`。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[目录对象 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[级别对象 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>另请参阅  
 [目录 (VB) 示例](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Caption 属性 (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Description 属性 (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName 属性 (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
