---
title: EndOfRecordset 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- EndOfRecordset
- Recordset::EndOfRecordset
helpviewer_keywords:
- EndOfRecordset event [ADO]
ms.assetid: 475de5e2-f634-4954-9edf-0027a6ba38d6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 414094da95076a7fb3781877645c5d43a03e6a7f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698217"
---
# <a name="endofrecordset-event-ado"></a>EndOfRecordset 事件 (ADO)
**EndOfRecordset**尝试移到末尾的行时调用事件[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
EndOfRecordset fMoreData, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *fMoreData*  
 一个**VARIANT_BOOL**值，如果设置为 VARIANT_TRUE，则指示更多的行已添加到**记录集**。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。  
  
 当**EndOfRecordset**是调用，此参数设置为**adStatusOK**引发该事件的操作是否成功。 设置为**adStatusCantDeny**如果此事件不能请求取消的引发此事件的操作。  
  
 之前**EndOfRecordset**返回时，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 一个**记录集**对象。 **记录集**有关发生此事件。  
  
## <a name="remarks"></a>备注  
 **EndOfRecordset**如果有可能发生事件[MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)操作将失败。  
  
 此事件处理程序调用时尝试跳过的最终**记录集**对象，这可能是因为调用**MoveNext**。 但是，在此情况下，您无法从数据库中检索多条记录并将它们追加到末尾**记录集**。 在这种情况下，设置*fMoreData*为 VARIANT_TRUE，并返回从**EndOfRecordset**。 然后调用**MoveNext**再次以访问新检索的记录。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
