---
title: 支持方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cce5ab3b735d3c641da4a6234e860d0528f107c2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67936703"
---
# <a name="supports-method"></a>Supports 方法
确定指定[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象支持特定类型的功能。  
  
## <a name="syntax"></a>语法  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>返回值  
 返回**布尔**值，该值指示是否所有功能标识*CursorOptions*提供程序支持参数。  
  
#### <a name="parameters"></a>Parameters  
 *CursorOptions*  
 一个**长**包含一个或多个表达式[CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md)值。  
  
## <a name="remarks"></a>备注  
 使用**支持**方法来确定哪些类型的功能**记录集**对象支持。 如果**记录集**对象支持的功能，其相应的常量是*CursorOptions*，则**支持**方法将返回**True**. 否则，它将返回**False**。  
  
> [!NOTE]
>  尽管**支持**方法可能会返回**True**对于给定的功能，它不保证，提供程序可以使该功能可在所有情况下。 **支持**方法仅返回满足某些条件的下提供程序是否支持指定的功能。 例如，**支持**方法可能指示**记录集**对象支持更新，即使光标基于多个表联接，其中某些列不是可更新。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Supports 方法示例 (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Supports 方法示例 （VC + +）](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [CursorType 属性 (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
