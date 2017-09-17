---
title: "Requery 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f59d4c6cdcdb3f34be4361969da15e5af117f995
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="requery-method"></a>Requery 方法
更新中的数据[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)通过重新执行的查询所基于的对象的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parameters  
 *选项*  
 可选。 包含一个位屏蔽[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)和[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)影响此操作的值。  
  
> [!NOTE]
>  如果*选项*设置为**adAsyncExecute**，将以异步方式执行此操作和[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)当它到结束，将发出事件。 **ExecuteOpenEnum**值**adExecuteNoRecords**或**adExecuteStream**不应与使用**Requery**。  
  
## <a name="remarks"></a>注释  
 使用**Requery**方法若要刷新的全部内容**记录集**重新颁发原始命令和检索第二次的数据的数据源的对象。 调用此方法等效于调用[关闭](../../../ado/reference/ado-api/close-method-ado.md)和[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)连续的方法。 如果你正在编辑当前记录或添加新记录时，发生错误。  
  
 虽然**记录集**对象处于打开状态，定义光标的性质的属性 ([游标类型](../../../ado/reference/ado-api/cursortype-property-ado.md)， [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)， [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)依此类推) 是只读的。 因此， **Requery**方法可以仅刷新当前光标。 若要更改任何游标属性并查看结果，必须使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法，以便再次属性变得读/写。 然后可以更改的属性设置和调用[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法重新打开光标。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [执行、 重新执行查询，并清除方法示例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [执行、 重新执行查询，并清除方法示例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、 重新执行查询，并清除方法示例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)

