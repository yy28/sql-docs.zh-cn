---
title: ISSAsynchStatus (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAsynchStatus (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a67b1efda62d76bd947dcbc9291f47be7f5f907d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015466"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
  **ISSAsynchStatus**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]异步操作。 这是一个可选接口继承自核心 OLE DB 接口**IDBAsynchStatus**。 除了**中止**和**GetStatus**方法继承自**IDBAsynchStatus**， **ISSAsynchStatus**提供了一个新方法用于等待异步操作已完成或发生超时。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](issasynchstatus-waitforasynchcompletion-ole-db.md)|等待，直到以异步方式执行的操作已完成或发生超时。|  
  
## <a name="remarks"></a>Remarks  
 **ISSAsynchStatus**实现**ISSAsynchStatus::GetStatus**方法等同于**IDBAsynchStatus::GetStatus**方法，但，如果数据源对象的初始化已中止，而不是 DB_E_CANCELED 返回 E_UNEXPECTED (尽管**ISSAsynchStatus::WaitForAsynchCompletion**返回 DB_E_CANCELED)。 这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [执行异步操作](../native-client/features/performing-asynchronous-operations.md)  
  
  