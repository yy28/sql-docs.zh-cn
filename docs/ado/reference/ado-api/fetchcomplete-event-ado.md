---
title: FetchComplete 事件 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7b5fb32f567dcfffb6112e843b53cb99a3b106bc
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697896"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 事件 (ADO)
**FetchComplete**耗时较长的异步操作中的所有记录到在都检索后，将调用事件[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了如果发生的错误的值**adStatus**是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 当调用此事件时，此参数设置为**adStatusOK**引发该事件的操作是否成功，或向**adStatusErrorsOccurred**如果操作失败。  
  
 此事件返回之前，请将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 一个**记录集**对象。 记录已为其检索到的对象。  
  
## <a name="remarks"></a>备注  
 若要使用**FetchComplete**使用 Microsoft Visual Basic、 Visual Basic 6.0 或更高版本是所需。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
