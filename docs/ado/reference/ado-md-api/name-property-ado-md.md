---
title: Name 属性（ADO MD） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 370dc7900e5fe876ea1b1064b2621371c730f323
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82765083"
---
# <a name="name-property-ado-md"></a>Name 属性 (ADO MD)
指示对象的名称。  
  
## <a name="return-values"></a>返回值  
 返回一个**字符串**，并且为只读。  
  
## <a name="remarks"></a>备注  
 可以按序号引用检索对象的**Name**属性，之后可以按名称直接引用对象。 例如，如果 `cdf.CubeDefs(0).Name` 生成 "Bobs-sfpreviewcluster Video Store"，则可以将此[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)称为 `cdf.CubeDefs("Bobs Video Store")` 。  
  
## <a name="applies-to"></a>应用于  
  
||||  
|-|-|-|  
|[轴对象 (ADO MD)](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|[目录对象 (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|[CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|  
|[维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|[级别对象 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|  
|[成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)|||  
  
## <a name="see-also"></a>另请参阅  
 [目录示例（VB）](../../../ado/reference/ado-md-api/catalog-example-vb.md)   
 [Caption 属性（ADO MD）](../../../ado/reference/ado-md-api/caption-property-ado-md.md)   
 [Description 属性（ADO MD）](../../../ado/reference/ado-md-api/description-property-ado-md.md)   
 [UniqueName 属性 (ADO MD)](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md)
