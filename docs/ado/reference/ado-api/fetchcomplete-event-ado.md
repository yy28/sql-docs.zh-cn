---
title: FetchComplete 事件（ADO） |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 850709dd8b4370360f5c06105266fb2c2510916c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82757123"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 事件 (ADO)
当长时间异步操作中的所有记录都已检索到[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)后，将调用**FetchComplete**事件。  
  
## <a name="syntax"></a>语法  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>参数  
 *pError*  
 一个[错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述了**adStatus**的值为**adStatusErrorsOccurred**时所发生的错误;否则，不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 当调用此事件时，如果导致事件的操作成功，则将此参数设置为**adStatusOK** ; 如果操作失败，则设置为**adStatusErrorsOccurred** 。  
  
 在此事件返回之前，将此参数设置为**adStatusUnwantedEvent**以防止后续通知。  
  
 *pRecordset*  
 **记录集**对象。 为其检索记录的对象。  
  
## <a name="remarks"></a>备注  
 若要将**FetchComplete**与 Microsoft Visual Basic 一起使用，需要 Visual Basic 6.0 或更高版本。  
  
## <a name="see-also"></a>另请参阅  
 [ADO 事件模型示例（VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
