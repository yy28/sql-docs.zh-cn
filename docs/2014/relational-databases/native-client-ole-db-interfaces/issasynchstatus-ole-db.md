---
title: ISSAsynchStatus (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a112c19d78c4d59b68ea5896109f88a101aaad13
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413399"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
  **ISSAsynchStatus**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]异步操作。 这是一个可选接口继承自核心 OLE DB 接口**IDBAsynchStatus**。 除了**中止**并**GetStatus**方法从继承**IDBAsynchStatus**， **ISSAsynchStatus**提供一种新方法用于等待，直到异步操作已完成或发生超时。  
  
|方法|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[Issasynchstatus:: Getstatus &#40;OLE DB&#41;](issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](issasynchstatus-waitforasynchcompletion-ole-db.md)|等待，直到异步执行的操作已完成或发生超时。|  
  
## <a name="remarks"></a>Remarks  
 **ISSAsynchStatus**的实现**issasynchstatus:: Getstatus**方法等同于**IDBAsynchStatus::GetStatus**方法，但，如果数据源对象的初始化已中止，将返回 E_UNEXPECTED，而不是 DB_E_CANCELED (尽管**issasynchstatus:: Waitforasynchcompletion**返回 DB_E_CANCELED)。 这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)   
 [执行异步操作](../native-client/features/performing-asynchronous-operations.md)  
  
  
