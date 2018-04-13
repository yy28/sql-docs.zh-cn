---
title: ISSAsynchStatus (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9055e0410deed0d77c1bf14554789e753d229ef7
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/24/2018
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSAsynchStatus**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]异步操作。 这是一个可选接口继承自核心 OLE DB 接口**IDBAsynchStatus**。 除了**中止**和**GetStatus**方法继承自**IDBAsynchStatus**， **ISSAsynchStatus**提供了一个新方法用于等待异步操作已完成或发生超时。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|等待，直到以异步方式执行的操作已完成或发生超时。|  
  
## <a name="remarks"></a>注释  
 **ISSAsynchStatus**实现**ISSAsynchStatus::GetStatus**方法等同于**IDBAsynchStatus::GetStatus**方法，但，如果数据源对象的初始化已中止，而不是 DB_E_CANCELED 返回 E_UNEXPECTED (尽管**ISSAsynchStatus::WaitForAsynchCompletion**返回 DB_E_CANCELED)。 这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另请参阅  
 [接口 & #40; OLE DB & #41;](http://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [执行异步操作](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
