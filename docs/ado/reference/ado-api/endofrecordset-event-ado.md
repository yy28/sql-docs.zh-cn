---
title: "EndOfRecordset 事件 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 79d37ae42a9c9e607ba4d8dba8917fccd7f20c42
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 事件 (ADO)
**EndOfRecordset**尝试移动到末尾的某一行时调用事件[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *fMoreData*  
 A **VARIANT_BOOL**值，如果设置为 VARIANT_TRUE，指示更多的行已添加到**记录集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**EndOfRecordset**是调用，此参数设置为**adStatusOK**引起该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消操作导致此事件。  
  
 之前**EndOfRecordset**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 A**记录集**对象。 **记录集**此事件发生的。  
  
## <a name="remarks"></a>注释  
 **EndOfRecordset**事件可能会发生如果[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)操作失败。  
  
 此事件处理程序时尝试移动的末尾调用**记录集**对象，可能是由于调用**MoveNext**。 但是，在此事件，你无法从数据库中检索多个记录，将它们追加到末尾**记录集**。 在这种情况下，设置*fMoreData* VARIANT_TRUE，并返回从**EndOfRecordset**。 然后调用**MoveNext**以访问新检索到的记录。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
