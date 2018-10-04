---
title: Name 属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
helpviewer_keywords:
- Name property [ADO MD]
ms.assetid: 4a04380b-51dc-4aaf-8d25-123cdd589641
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5c6c9ba7f2981fd4162f93f37e6ad0eb2cbae882
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756762"
---
# <a name="name-property-ado-md"></a>Name 属性 (ADO MD)
指示一个对象的名称。  
  
## <a name="return-values"></a>返回值  
 返回**字符串**和是只读的。  
  
## <a name="remarks"></a>备注  
 可以检索**名称**序号引用，然后可以直接通过名称引用该对象由对象的属性。 例如，如果`cdf.CubeDefs(0).Name`产生"Bobs 视频 Store"，可以参考此[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)作为`cdf.CubeDefs("Bobs Video Store")`。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[目录对象 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[级别对象 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>请参阅  
 [目录示例 (VB)](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Caption 属性 (ADO MD)](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Description 属性 (ADO MD)](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName 属性 (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
