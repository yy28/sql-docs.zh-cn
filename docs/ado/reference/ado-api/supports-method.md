---
description: Supports 方法
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ea56dc34cc2c69c7bb9ef30433a6c7c75f26c552
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777116"
---
# <a name="supports-method"></a>Supports 方法
确定指定的 [记录集](./recordset-object-ado.md) 对象是否支持特定类型的功能。  
  
## <a name="syntax"></a>语法  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>返回值  
 返回一个 **布尔** 值，该值指示提供程序是否支持由 *CursorOptions* 参数标识的所有功能。  
  
#### <a name="parameters"></a>parameters  
 *CursorOptions*  
 包含一个或多个[CursorOptionEnum](./cursoroptionenum.md)值的**长**表达式。  
  
## <a name="remarks"></a>备注  
 使用 **支持** 方法可以确定 **Recordset** 对象支持的功能类型。 如果 **Recordset** 对象支持其对应常量在 *CursorOptions*中的功能，则 **支持** 方法返回 **True**。 否则，返回 **False**。  
  
> [!NOTE]
>  尽管 **支持** 方法对于给定的功能可能会返回 **True** ，但并不保证提供程序在所有情况下都可以使用该功能。 如果满足某些条件，则 **支持** 方法只返回提供程序是否可以支持指定的功能。 例如， **支持** 方法可能指示 **Recordset** 对象支持更新，即使游标基于多表联接，某些列是不可更新的。  
  
## <a name="applies-to"></a>适用于  
 [记录集对象 (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (VB 支持方法示例) ](./supports-method-example-vb.md)   
 [ (VC + + 支持方法示例) ](./supports-method-example-vc.md)   
 [CursorType 属性 (ADO)](./cursortype-property-ado.md)