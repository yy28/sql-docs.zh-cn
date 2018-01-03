---
title: "Description 属性 (ADO MD) |Microsoft 文档"
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
- Member::Description
- Level::Description
- CubeDef::Description
- Hierarchy::Description
- Description
- Dimension::Description
helpviewer_keywords: Description property [ADO MD]
ms.assetid: 6d626d35-0bf3-4f24-9934-ad9c9c91273a
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 173b5c3ac03ad7a472fa3e0f82617da20f281d73
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="description-property-ado-md"></a>Description 属性 (ADO MD)
返回当前对象的文本说明。  
  
## <a name="return-values"></a>返回值  
 返回**字符串**和是只读的。  
  
## <a name="remarks"></a>Remarks  
 有关[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象，**说明**仅适用于度量值和公式的成员。 **说明**返回空字符串 ("") 对于所有其他类型的成员。 有关各种类型的成员的详细信息，请参阅[类型](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性。  
  
 在上才支持此属性**成员**属于对象[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象。 从引用此属性时出现错误**成员**属于对象[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象。  
  
## <a name="applies-to"></a>适用范围  
  
||||  
|-|-|-|  
|[CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[级别对象 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
