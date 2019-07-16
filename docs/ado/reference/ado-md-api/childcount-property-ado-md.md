---
title: ChildCount 属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ChildCount
- Member::ChildCount
helpviewer_keywords:
- ChildCount property [ADO MD]
ms.assetid: 5463be22-ca50-43ea-9c92-468fc8eda280
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a8e6f6a7cb749ff2b22a1f7563b43ce07e060aab
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67911557"
---
# <a name="childcount-property-ado-md"></a>ChildCount 属性 (ADO MD)
指示为其成员的当前[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象是父对象的层次结构中。  
  
## <a name="return-values"></a>返回值  
 返回**长**整数和是只读的。  
  
## <a name="remarks"></a>备注  
 使用**ChildCount**属性以返回多少个子级的估计**成员**具有。 实际的子级**成员**可以返回由[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)属性。  
  
 有关**成员**中的对象[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象，返回的最大数目为 65536。 如果子级的实际数目超过 65536，返回的值将仍是小于 65536。 因此，应用程序应如何解释**ChildCount**的等于或大于 65536 子级为 65536。  
  
 有关**成员**中的对象[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象，请使用 ADO 集合[计数](../../../ado/reference/ado-api/count-property-ado.md)属性**子级**集合以确定子级的精确数目。 确定的子级的精确数目可能会很慢，如果集合中的子级的数量很大。  
  
## <a name="applies-to"></a>适用范围  
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>请参阅  
 [Children 属性 (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count 属性 (ADO)](../../../ado/reference/ado-api/count-property-ado.md)   
 [成员集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
