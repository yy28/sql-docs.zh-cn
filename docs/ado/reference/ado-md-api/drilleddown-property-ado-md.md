---
title: "DrilledDown 属性 (ADO MD) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- DrilledDown
- Member::DrilledDown
helpviewer_keywords:
- DrilledDown property [ADO MD]
ms.assetid: bf39dd36-fc7a-4f6e-86c0-fa71430c0d86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8dfa880e78bdeccf722723a7d05f2f0ca1938ed6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="drilleddown-property-ado-md"></a>DrilledDown 属性 (ADO MD)
该值指示是否立即跟随子级[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)在轴上。  
  
## <a name="return-values"></a>返回值  
 返回**布尔**值并且是只读的。 **DrilledDown**返回**True**如果没有在轴上的当前成员的子成员。 **DrilledDown**返回**False**如果当前的成员具有在轴上的一个或多个子成员。  
  
## <a name="remarks"></a>注释  
 使用**DrilledDown**属性来确定是否存在紧跟此成员在轴上的此成员的至少一个子级。 显示该成员时，此信息很有用。  
  
 在上才支持此属性[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)属于对象[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象。 从引用此属性时出现错误**成员**属于对象[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象。  
  
## <a name="applies-to"></a>适用范围  
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ParentSameAsPrev 属性 (ADO MD)](../../../ado/reference/ado-md-api/parentsameasprev-property-ado-md.md)
