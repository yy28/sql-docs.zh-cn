---
title: LockType 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::LockType
helpviewer_keywords:
- LockType property [ADO]
ms.assetid: 9920c14e-033a-4de1-8149-0ce9737a3246
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05670439a8f14018a999557dd135912e0c2e0159
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47736015"
---
# <a name="locktype-property-ado"></a>LockType 属性 (ADO)
指示在编辑期间记录上放置锁的类型。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值。 默认值是**adLockReadOnly**。  
  
## <a name="remarks"></a>备注  
 设置**LockType**打开之前的属性[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)指定打开它时，应使用哪种类型的锁定该提供程序。 要返回的锁定中使用的一种开放类型的属性中读取**记录集**对象。  
  
 提供程序可能不支持所有的锁类型。 如果提供程序无法支持请求**LockType**设置，它将替换为另一种类型的锁定。 若要确定在可用的实际锁定功能**记录集**对象，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法替换**adUpdate**和**adUpdateBatch**.  
  
 **AdLockPessimistic**如果不支持设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。 如果设置不支持的值，则会不产生任何错误;最接近的支持**LockType**将改为使用。  
  
 **LockType**属性为读/写时**记录集**打开时为已关闭，只读的。  
  
> [!NOTE]
>  **远程数据服务使用情况**客户端上使用时**记录集**对象， **LockType**属性只能设置为**adLockBatchOptimistic**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [CursorType、 LockType、 和 EditMode 属性示例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、 LockType、 和 EditMode 属性示例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch 方法 (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
