---
title: CursorType 属性（ADO） |Microsoft Docs
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
ms.openlocfilehash: 4dc881b96a1e2641d4946340c9462455197f2043
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67919248"
---
# <a name="cursortype-property-ado"></a>CursorType 属性 (ADO)
指示[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象中使用的游标的类型。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值。 默认值为**adOpenForwardOnly**。  
  
## <a name="remarks"></a>备注  
 使用**CursorType**属性可以指定在打开**Recordset**对象时应使用的游标类型。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**，则仅支持**adOpenStatic**的设置。 如果设置了不受支持的值，则不会产生错误;将改用最近支持的**CursorType** 。  
  
 如果提供程序不支持所请求的游标类型，则它可能返回另一个游标类型。 当[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象处于打开状态时， **CursorType**属性将更改以匹配实际使用的游标类型。 若要验证返回的游标的特定功能，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法。 关闭**记录集**后， **CursorType**属性将恢复为其原始设置。  
  
 下图显示了每个游标类型所需的提供程序功能（由**支持**的方法常量标识）。  
  
|对于此 CursorType 的记录集|对于所有这些常量，支持方法必须返回 True|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**、 **adHoldRecords**、 **adMovePrevious**、 **adResync**|  
  
> [!NOTE]
>  虽然对于动态和只进游标，**支持**（**adUpdateBatch**）可能是 true，但对于批处理更新，应使用键集或静态游标。 将[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)属性设置为**AdLockBatchOptimistic** ，将**CursorLocation**属性设置为**adUseClient** ，以便为批更新启用 OLE DB 的游标服务。  
  
 当**记录集**关闭时， **CursorType**属性是可读/写的。  
  
> [!NOTE]
>  **远程数据服务使用情况**在客户端**记录集**对象上使用时，只能将**CursorType**属性设置为**adOpenStatic**。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CursorType、LockType 和 EditMode 属性示例（VB）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType 和 EditMode 属性示例（VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
