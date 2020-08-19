---
description: Requery 方法
title: Requery 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: rothja
ms.author: jroth
ms.openlocfilehash: b13d618bf5b9b2c17a4fd93b08f3a861cb958178
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88442319"
---
# <a name="requery-method"></a>Requery 方法
通过重新执行对象所基于的查询来更新 [记录集](../../../ado/reference/ado-api/recordset-object-ado.md) 对象中的数据。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>参数  
 *选项*  
 可选。 一个位掩码，其中包含影响此操作的 [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) 和 [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) 值。  
  
> [!NOTE]
>  如果 *选项* 设置为 **adAsyncExecute**，此操作将以异步方式执行，并且在结束时将发出 [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) 事件。 **AdExecuteNoRecords**或**adExecuteStream**的**ExecuteOpenEnum**值不应与**Requery**一起使用。  
  
## <a name="remarks"></a>备注  
 使用 **Requery** 方法，通过重新发出原始命令并再次检索数据来刷新数据源的 **记录集** 对象的全部内容。 调用此方法等效于连续调用 [Close](../../../ado/reference/ado-api/close-method-ado.md) 和 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 方法。 如果正在编辑当前记录或添加新记录，则会发生错误。  
  
 **Recordset**对象处于打开状态时，定义游标性质的属性 ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)、 [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)、 [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)等) 为只读。 因此， **Requery** 方法只能刷新当前游标。 若要更改任何游标属性并查看结果，必须使用 [Close](../../../ado/reference/ado-api/close-method-ado.md) 方法，使属性再次变为读/写。 然后，可以更改属性设置并调用 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 方法以重新打开光标。  
  
## <a name="applies-to"></a>适用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行、再次查询和清除方法示例 (VB) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [ (VBScript) 执行、再次查询和清除方法示例 ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、再次查询和清除方法示例 (VC + +) ](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
