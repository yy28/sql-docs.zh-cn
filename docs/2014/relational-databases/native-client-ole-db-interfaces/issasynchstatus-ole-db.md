---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
author: rothja
ms.author: jroth
ms.openlocfilehash: 4489f9d1ad576d49d885842f6969f9b61065791c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056132"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
  **ISSAsynchStatus**公开对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 异步操作的支持。 这是一个可选接口，它继承自 core OLE DB interface **IDBAsynchStatus**。 除了从 IDBAsynchStatus 继承的 Abort 和 GetStatus 方法外，ISSAsynchStatus 还提供一个新方法，用于在完成异步操作或发生超时前等待****************。  
  
|方法|说明|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](issasynchstatus-waitforasynchcompletion-ole-db.md)|一直等待，直到异步执行的操作完成或发生超时。|  
  
## <a name="remarks"></a>备注  
 ISSAsynchStatus::GetStatus 方法的 ISSAsynchStatus 实现与 IDBAsynchStatus::GetStatus 方法大体相同，不同之处在于如果中止对数据源对象的初始化，前者将返回 E_UNEXPECTED，而不是 DB_E_CANCELED（但是 ISSAsynchStatus::WaitForAsynchCompletion 将返回 DB_E_CANCELED）****************。 这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [执行异步操作](../native-client/features/performing-asynchronous-operations.md)  
  
  
