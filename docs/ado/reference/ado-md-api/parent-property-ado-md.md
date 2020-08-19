---
description: Parent 属性 (ADO MD)
title: 父属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Parent
- Member::Parent
helpviewer_keywords:
- Parent property [ADO MD]
ms.assetid: 32c278c1-d8e1-4bb7-9ecd-2fbfdffee34b
author: rothja
ms.author: jroth
ms.openlocfilehash: 4c599bd75388dc0b2ea7e4a5c16f495817f917ba
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440789"
---
# <a name="parent-property-ado-md"></a>Parent 属性 (ADO MD)
指示作为层次结构中当前 [成员](../../../ado/reference/ado-md-api/member-object-ado-md.md) 的父成员的成员。  
  
## <a name="return-values"></a>返回值  
 返回一个 [成员](../../../ado/reference/ado-md-api/member-object-ado-md.md) 对象，并且是只读的。  
  
## <a name="remarks"></a>备注  
 位于层次结构顶层 (根) 的成员没有父项。 此属性仅在属于某一[级别](../../../ado/reference/ado-md-api/level-object-ado-md.md)对象的**成员**对象上受支持。 从属于某个[位置](../../../ado/reference/ado-md-api/position-object-ado-md.md)对象的**成员**对象引用此属性时，将发生错误。  
  
## <a name="applies-to"></a>适用于  
 [成员对象 (ADO MD)](../../../ado/reference/ado-md-api/member-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [Children 属性 (ADO MD)](../../../ado/reference/ado-md-api/children-property-ado-md.md)
