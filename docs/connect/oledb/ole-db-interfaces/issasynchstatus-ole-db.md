---
title: ISSAsynchStatus (OLE DB) |Microsoft 文档
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-interfaces
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
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: ca37010f2c0c0e42dd7e75f2dc87b0654fb31474
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSAsynchStatus**接口公开支持[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]异步操作。 它是一个可选接口继承自核心 OLE DB 接口**IDBAsynchStatus**。 除了**中止**和**GetStatus**方法继承自**IDBAsynchStatus**， **ISSAsynchStatus**提供了一个新方法用于等待异步操作已完成或发生超时。  
  
|方法|Description|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|等待，直到以异步方式执行的操作已完成或发生超时。|  
  
## <a name="remarks"></a>注释  
 **ISSAsynchStatus**实现**ISSAsynchStatus::GetStatus**方法等同于**IDBAsynchStatus::GetStatus**方法，但，如果数据源对象的初始化已中止，而不是 DB_E_CANCELED 返回 E_UNEXPECTED (尽管**ISSAsynchStatus::WaitForAsynchCompletion**返回 DB_E_CANCELED)。 这是因为数据源对象未处于以下中止操作，常用状态，以便进一步初始化操作可能已尝试。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另请参阅  
 [接口 & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [执行异步操作](../../oledb/features/performing-asynchronous-operations.md)  
  
  
