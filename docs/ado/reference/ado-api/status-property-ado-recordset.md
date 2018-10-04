---
title: 状态属性 （ADO 记录集） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::GetStatus
- Recordset15::Status
helpviewer_keywords:
- Status property [ADO Recordset]
ms.assetid: 41d70d89-880f-4850-9d17-19d9790cc8eb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5847300af48b39dc12ccb65f5e03f1fdc6f8e795
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822075"
---
# <a name="status-property-ado-recordset"></a>Status 属性（ADO 记录集）
指示相对于批处理更新的当前记录或其他大容量操作的状态。  
  
## <a name="return-value"></a>返回值  
 返回一个或多个总和[RecordStatusEnum](../../../ado/reference/ado-api/recordstatusenum.md)值。  
  
## <a name="remarks"></a>备注  
 使用**状态**属性以查看哪些更改处于挂起状态的批更新过程中修改的记录。 此外可以使用**状态**属性以查看在大容量操作，例如当你调用期间失败的记录的状态[重新同步](../../../ado/reference/ado-api/resync-method.md)， [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)，或者[CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md)上的方法[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象，或者设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性**记录集**书签为数组的对象。 通过此属性，您可以确定给定的记录如何失败，并相应地进行解决。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Status 属性示例 （记录集） (VB)](../../../ado/reference/ado-api/status-property-example-recordset-vb.md)   
 [State 属性示例 (VC++)](../../../ado/reference/ado-api/status-property-example-vc.md)   
