---
title: Children 属性 (ADO MD) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Member::Children
- Children
helpviewer_keywords:
- Children property [ADO MD]
ms.assetid: 61d36468-1ccd-467a-9cb5-17d0bfacc766
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0ca7bff8aae165833dcf6e0cc20bd1af55d62279
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35283536"
---
# <a name="children-property-ado-md"></a>Children 属性 (ADO MD)
返回[成员](../../../ado/reference/ado-md-api/members-collection-ado-md.md)为其集合当前[成员](../../../ado/reference/ado-md-api/member-object-ado-md.md)是层次结构中的父级。  
  
## <a name="return-values"></a>返回值  
 返回**成员**集合是只读的和。  
  
## <a name="remarks"></a>Remarks  
 **子级**属性包含**成员**为其集合当前**成员**是分层的父级。 叶级别**成员**对象在中有任何子成员**成员**集合。 在上才支持此属性**成员**属于对象[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象。 从引用此属性时出现错误**成员**属于对象[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象。  
  
## <a name="applies-to"></a>适用范围  
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>请参阅  
 [ChildCount 属性 (ADO MD)](../../../ado/reference/ado-md-api/childcount-property-ado-md.md)
