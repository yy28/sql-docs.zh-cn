---
title: "游标类型属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::CursorType
helpviewer_keywords: CursorType property [ADO]
ms.assetid: b62c66ca-58d5-430e-9257-eb38c65e48c2
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3f1f16755e5030cec19d7b513f725f3fd5defb3f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="cursortype-property-ado"></a>游标类型属性 (ADO)
指示在中使用的游标类型[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[CursorTypeEnum](../../../ado/reference/ado-api/cursortypeenum.md)值。 默认值是**adOpenForwardOnly**。  
  
## <a name="remarks"></a>注释  
 使用**游标类型**属性指定的一种打开时应使用的游标**记录集**对象。  
  
 仅设置**adOpenStatic**如果，则支持[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 如果设置不支持的值，则不会产生错误;最近支持**游标类型**将改为使用。  
  
 如果提供程序不支持请求的游标类型，它可能返回另一个游标类型。 **游标类型**属性将更改以匹配实际游标类型中使用时[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象处于打开状态。 若要验证特定功能返回的光标，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法。 关闭后**记录集**、**游标类型**属性会恢复为其原始设置。  
  
 下图显示了提供程序功能 (由标识**支持**方法常量) 所需的每种游标类型。  
  
|为此游标类型的记录集|这些常量的所有支持方法必须返回 True|  
|----------------------------------------|---------------------------------------------------------------------|  
|**adOpenForwardOnly**|none|  
|**adOpenKeyset**|**adBookmark**， **adHoldRecords**， **adMovePrevious**， **adResync**|  
|**adOpenDynamic**|**adMovePrevious**|  
|**adOpenStatic**|**adBookmark**， **adHoldRecords**， **adMovePrevious**， **adResync**|  
  
> [!NOTE]
>  尽管**支持**(**adUpdateBatch**) 的可能是为动态和只进游标，批处理更新你应使用键集或静态游标。 设置[LockType](../../../ado/reference/ado-api/locktype-property-ado.md)属性**adLockBatchOptimistic**和**CursorLocation**属性**adUseClient**启用光标用于 OLE DB，所需的批处理更新的服务。  
  
 **游标类型**属性为读/写时**记录集**打开时为已关闭，只读的。  
  
> [!NOTE]
>  **远程数据服务使用情况**时在客户端上使用**记录集**对象，**游标类型**属性可以将仅为**adOpenStatic**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [游标类型、 LockType，以及 EditMode 属性示例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [游标类型、 LockType 和 EditMode 属性示例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [Supports 方法](../../../ado/reference/ado-api/supports-method.md)
