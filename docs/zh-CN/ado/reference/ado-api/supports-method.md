---
title: 支持方法 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0132c3742d7e85f198cd0453fb45064cebeae542
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="supports-method"></a>支持方法
确定指定[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象支持特定类型的功能。  
  
## <a name="syntax"></a>语法  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>返回值  
 返回**布尔**值，该值指示是否将的所有功能标识*CursorOptions*自变量受提供程序。  
  
#### <a name="parameters"></a>Parameters  
 *CursorOptions*  
 A**长**表达式包含一个或多个[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)值。  
  
## <a name="remarks"></a>注释  
 使用**支持**方法来确定哪些类型的功能**记录集**对象支持。 如果**记录集**对象支持的功能，其相应常量位于*CursorOptions*、**支持**方法返回**True**. 否则，它将返回**False**。  
  
> [!NOTE]
>  尽管**支持**方法可能返回**True**对于给定的功能，它无法保障，该提供程序可以使该功能可在所有情况下。 **支持**方法只返回满足某些条件的下提供程序是否支持指定的功能。 例如，**支持**方法可能表明**记录集**对象支持更新，即使光标基于多个表联接，其中某些列不能更新。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [支持方法示例 (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [支持方法示例 （VC + +）](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType 属性 (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
