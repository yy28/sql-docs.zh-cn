---
title: ChildCount 属性（ADO MD） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67911557"
---
# <a name="childcount-property-ado-md"></a>ChildCount 属性 (ADO MD)
指示当前[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)对象作为层次结构中的父级的成员的数目。  
  
## <a name="return-values"></a>返回值  
 返回一个**长**整型，并且为只读。  
  
## <a name="remarks"></a>备注  
 使用**ChildCount**属性可以返回某个**成员**具有的子级数量的估计值。 **成员**的实际子级可以由[子级](../../../ado/reference/ado-md-api/children-property-ado-md.md)属性返回。  
  
 对于[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象中的**成员**对象，返回的最大值为65536。 如果子项的实际数目超过65536，则返回的值仍为65536。 因此，应用程序应将65536的**ChildCount**解释为等于或大于65536子级。  
  
 对于[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象中的**成员**对象，请使用**子**集合上的 "ADO 集合[计数](../../../ado/reference/ado-api/count-property-ado.md)" 属性来确定确切的子项数。 如果集合中的子级数量很大，确定子项的确切数目可能会很慢。  
  
## <a name="applies-to"></a>应用于  
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [子属性（ADO MD）](../../../ado/reference/ado-md-api/children-property-ado-md.md)   
 [Count 属性（ADO）](../../../ado/reference/ado-api/count-property-ado.md)   
 [成员集合 (ADO MD)](../../../ado/reference/ado-md-api/members-collection-ado-md.md)
