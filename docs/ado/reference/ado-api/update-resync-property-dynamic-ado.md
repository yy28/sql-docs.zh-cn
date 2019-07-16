---
title: 更新 Resync 属性-动态 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Update Resync property [ADO]
ms.assetid: 8a3bb608-66d7-4128-a3ef-84cb0556de0d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed0e3ad8027c31a351ddb4506d3b420aa3a1124d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938808"
---
# <a name="update-resync-property-dynamic-ado"></a>Update Resync 属性 - 动态 (ADO)
指定是否[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法后跟一个隐式[重新同步](../../../ado/reference/ado-api/resync-method.md)方法操作，如果是，该操作的范围。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个或多个[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)值。  
  
## <a name="remarks"></a>备注  
 除了 adResyncAll 已表示其余值的组合，可能会组合 ADCPROP_UPDATERESYNC_ENUM 的值。  
  
 常量**adResyncConflicts**存储的重新同步值作为基础值，但不会覆盖挂起的更改。  
  
 **更新重新同步**动态属性追加到[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象[属性](../../../ado/reference/ado-api/properties-collection-ado.md)集合时[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
