---
title: Description 属性 (ADO MD) |Microsoft 文档
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
apitype: COM
f1_keywords:
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords:
- Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7136df5847753cded0ed8d735bf64f9d2dc90b79
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="description-property-ado-md"></a>Description 属性 (ADO MD)
返回当前对象的文本说明。  
  
## <a name="return-values"></a>返回值  
 返回**字符串**和是只读的。  
  
## <a name="remarks"></a>注释  
 有关[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象，**说明**仅适用于度量值和公式的成员。 **说明**返回空字符串 ("") 对于所有其他类型的成员。 有关各种类型的成员的详细信息，请参阅[类型](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性。  
  
 在上才支持此属性**成员**属于对象[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象。 从引用此属性时出现错误**成员**属于对象[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[级别对象 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
