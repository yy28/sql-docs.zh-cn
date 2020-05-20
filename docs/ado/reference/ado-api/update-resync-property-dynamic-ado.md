---
title: 更新重新同步属性-动态（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: e9d000150cc86a8c838ac5dea827b5c376f3a79f
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759483"
---
# <a name="update-resync-property-dynamic-ado"></a>Update Resync 属性 - 动态 (ADO)
指定[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法是否后跟隐式重新[同步](../../../ado/reference/ado-api/resync-method.md)方法操作，如果是，则为该操作的范围。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个或多个[ADCPROP_UPDATERESYNC_ENUM](../../../ado/reference/ado-api/adcprop-updateresync-enum.md)值。  
  
## <a name="remarks"></a>备注  
 ADCPROP_UPDATERESYNC_ENUM 的值可以组合在一起，但 adResyncAll 的值已表示剩余值的组合。  
  
 常量**adResyncConflicts**将重新同步值作为基础值存储，但不会覆盖挂起的更改。  
  
 当[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**AdUseClient**时，**更新重新同步**是追加到[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)对象[Properties](../../../ado/reference/ado-api/properties-collection-ado.md) collection 的动态属性。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
