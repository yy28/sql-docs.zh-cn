---
title: CursorType 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CursorType
helpviewer_keywords:
- CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7361b453272289107ea3c5ae268b951178aa1b43
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695506"
---
# <a name="cursortype-property-ado"></a>CursorType 属性 (ADO)
指示使用中的游标类型[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值。 默认值是**adOpenForwardOnly**。  
  
## <a name="remarks"></a>备注  
 使用**CursorType**属性指定的游标打开时应使用的类型**记录集**对象。  
  
 仅设置**adOpenStatic**如果，则支持[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 如果设置不支持的值，则会不产生任何错误;最接近的支持**CursorType**将改为使用。  
  
 如果提供程序不支持请求的游标类型，它可能返回另一个游标类型。 **CursorType**属性将更改以匹配实际游标类型在使用时[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象处于打开状态。 若要验证返回的游标的特定功能，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法。 关闭后**记录集**，则**CursorType**属性恢复为原始设置。  
  
 下图显示了提供程序功能 (由标识**支持**方法常量) 所需的每个游标类型。  
  
|此游标类型的记录集|这些常量的所有支持方法必须返回 True|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**， **adHoldRecords**， **adMovePrevious**， **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**， **adHoldRecords**， **adMovePrevious**， **adResync**|  
  
> [!NOTE]
>  尽管**支持**(**adUpdateBatch**) 批处理更新你的条件为真动态游标和只进游标，则应使用 keyset 或 static 游标。 设置[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)属性设置为**adLockBatchOptimistic**并**CursorLocation**属性设置为**adUseClient**启用光标对于 OLE DB，所需的批处理更新的服务。  
  
 **CursorType**属性为读/写时**记录集**打开时为已关闭，只读的。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**记录集**对象， **CursorType**可以将属性设置为仅**adOpenStatic**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [CursorType、 LockType、 和 EditMode 属性示例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、 LockType、 和 EditMode 属性示例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
