---
title: Description 属性（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5636b5f4e49ff9a5bbe46937a8d7b972e61b4502
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67938578"
---
# <a name="description-property-ado-md"></a>Description 属性 (ADO MD)
返回当前对象的文本说明。  
  
## <a name="return-values"></a>返回值  
 返回一个**字符串**，并且为只读。  
  
## <a name="remarks"></a>备注  
 对于[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象， **Description**仅适用于度量值和公式成员。 **Description**为所有其他类型的成员返回空字符串（""）。 有关各种类型成员的详细信息，请参阅[Type](../../../ado/reference/ado-md-api/type-property-ado-md.md)属性。  
  
 此属性仅在属于[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象的**成员**对象上受支持。 从属于某个[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象的**成员**对象引用此属性时，将发生错误。  
  
## <a name="applies-to"></a>应用于  
  
||||  
|-|-|-|  
|[CubeDef 对象 (ADO MD)](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|[维度对象 (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|[层次结构对象 (ADO MD)](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|  
|[级别对象 (ADO MD)](../../../ado/reference/ado-md-api/level-object-ado-md.md)|[成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)||
