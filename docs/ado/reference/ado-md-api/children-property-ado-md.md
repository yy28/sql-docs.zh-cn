---
title: 子属性（ADO MD） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cbec9733044127d23e75364697a41ccd7e8910e4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67911522"
---
# <a name="children-property-ado-md"></a>Children 属性 (ADO MD)
返回一个[成员](../../../ado/reference/ado-md-api/members-collection-ado-md.md)集合，其中的当前[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)是层次结构中的父级。  
  
## <a name="return-values"></a>返回值  
 返回**成员**集合，它是只读的。  
  
## <a name="remarks"></a>备注  
 **子**属性包含**成员**集合，该集合的当前**成员**为其层次结构父级。 叶级**成员**对象在**members**集合中没有子成员。 此属性仅在属于某一[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象的**成员**对象上受支持。 从属于某个[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象的**成员**对象引用此属性时，将发生错误。  
  
## <a name="applies-to"></a>应用于  
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [ChildCount 属性 (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
