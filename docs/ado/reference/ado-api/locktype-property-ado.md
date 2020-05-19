---
title: LockType 属性（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4a8d0f94d4482649030561f2ac71ed6de1374e46
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82754489"
---
# <a name="locktype-property-ado"></a>LockType 属性 (ADO)
指示在编辑过程中放置在记录上的锁的类型。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值。 默认值为**adLockReadOnly**。  
  
## <a name="remarks"></a>备注  
 在打开[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)之前设置**LockType**属性，以指定提供程序在打开它时应使用哪种类型的锁定。 读取属性，返回在打开的**记录集**对象上使用的锁定类型。  
  
 提供程序可能不支持所有锁定类型。 如果提供程序不支持请求的**LockType**设置，它将替换另一种类型的锁定。 若要确定**Recordset**对象中可用的实际锁定功能，请使用[支持](../../../ado/reference/ado-api/supports-method.md)方法和**adUpdate**和**adUpdateBatch**。  
  
 如果[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**，则不支持**adLockPessimistic**设置。 如果设置了不受支持的值，则不会产生错误;将改用最近支持的**LockType** 。  
  
 当**记录集**关闭时， **LockType**属性是可读/写的。  
  
> [!NOTE]
>  **远程数据服务使用情况**在客户端**记录集**对象上使用时，只能将**LockType**属性设置为**adLockBatchOptimistic**。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CursorType、LockType 和 EditMode 属性示例（VB）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType 和 EditMode 属性示例（VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [CancelBatch 方法（ADO）](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [UpdateBatch 方法](../../../ado/reference/ado-api/updatebatch-method.md)
