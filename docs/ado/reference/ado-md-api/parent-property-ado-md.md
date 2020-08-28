---
description: Parent 属性 (ADO MD)
title: 父属性 (ADO MD) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 93d7d550c4d70f207c3ab0fdeea0fa4ab0812c79
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88986208"
---
# <a name="parent-property-ado-md"></a>Parent 属性 (ADO MD)
指示作为层次结构中当前 [成员](./member-object-ado-md.md) 的父成员的成员。  
  
## <a name="return-values"></a>返回值  
 返回一个 [成员](./member-object-ado-md.md) 对象，并且是只读的。  
  
## <a name="remarks"></a>注解  
 位于层次结构顶层 (根) 的成员没有父项。 此属性仅在属于某一[级别](./level-object-ado-md.md)对象的**成员**对象上受支持。 从属于某个[位置](./position-object-ado-md.md)对象的**成员**对象引用此属性时，将发生错误。  
  
## <a name="applies-to"></a>适用于  
 [成员对象 (ADO MD)](./member-object-ado-md.md)  
  
## <a name="see-also"></a>另请参阅  
 [Children 属性 (ADO MD)](./children-property-ado-md.md)