---
title: DrilledDown 属性（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
author: rothja
ms.author: jroth
ms.openlocfilehash: c5819609f06b37ffad08918968530b66df169c64
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764258"
---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 属性 (ADO MD)
指示子元素是否紧靠在轴上的[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)后面。  
  
## <a name="return-values"></a>返回值  
 返回**布尔**值并且是只读的。 如果轴上的当前成员没有子成员，则**DrilledDown**将返回**True** 。 如果当前成员在轴上有一个或多个子成员，则**DrilledDown**将返回**False** 。  
  
## <a name="remarks"></a>备注  
 使用**DrilledDown**属性可确定紧靠此成员之后，在轴上是否至少有一个此成员的子级。 显示成员时，此信息很有用。  
  
 此属性仅在属于某个[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象的[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象上受支持。 从属于[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象的**成员**对象引用此属性时，将发生错误。  
  
## <a name="applies-to"></a>应用于  
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ParentSameAsPrev 属性 (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
