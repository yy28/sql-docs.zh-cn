---
title: FetchComplete 事件 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset::ExecuteComplete
- ExecuteComplete
helpviewer_keywords:
- FetchComplete event [ADO]
ms.assetid: a28d3858-566c-468d-b070-d1de4339fbea
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6d8024a302d76ad01aa3044c675fc2a42c7c7ed
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35278146"
---
# <a name="fetchcomplete-event-ado"></a>FetchComplete 事件 (ADO)
**FetchComplete**较长的异步操作中的所有记录已经都检索到后，将调用事件[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
FetchComplete pError, adStatus, pRecordset  
```  
  
#### <a name="parameters"></a>Parameters  
 *pError*  
 [错误](../../../ado/reference/ado-api/error-object.md)对象。 它描述发生错误的值**adStatus**是**adStatusErrorsOccurred**; 不会设置。  
  
 *adStatus*  
 [EventStatusEnum](../../../ado/reference/ado-api/eventstatusenum.md)状态值。 当调用此事件时，此参数设置为**adStatusOK**引起该事件的操作是否成功，或到**adStatusErrorsOccurred**如果操作失败。  
  
 此事件返回之前，将此参数设置为**adStatusUnwantedEvent**以防止后续的通知。  
  
 *pRecordset*  
 A**记录集**对象。 记录已为其检索到的对象。  
  
## <a name="remarks"></a>Remarks  
 若要使用**FetchComplete**与 Microsoft Visual Basic 中，Visual Basic 6.0 或更高版本是所需。  
  
## <a name="see-also"></a>请参阅  
 [ADO 事件模型示例 （VC + +）](../../../ado/reference/ado-api/ado-events-model-example-vc.md)   
 [ADO 事件处理程序摘要](../../../ado/guide/data/ado-event-handler-summary.md)
