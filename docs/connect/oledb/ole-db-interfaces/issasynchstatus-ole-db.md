---
title: ISSAsynchStatus (OLE DB) |Microsoft Docs
description: ISSAsynchStatus (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-interfaces
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
ms.openlocfilehash: 6c94fe229ab8b00ded7e0d32f45e6e2de8cdaaf4
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39105783"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  ISSAsynchStatus 公接口开对 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 异步操作的支持。 这一可选接口继承自核心 OLE DB 接口 IDBAsynchStatus。 除了从 IDBAsynchStatus 继承的 Abort 和 GetStatus 方法外，ISSAsynchStatus 还提供一个新方法，用于在完成异步操作或发生超时前等待。  
  
|方法|描述|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[Issasynchstatus:: Getstatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|一直等待，直到异步执行的操作完成或发生超时。|  
  
## <a name="remarks"></a>Remarks  
 ISSAsynchStatus::GetStatus 方法的 ISSAsynchStatus 实现与 IDBAsynchStatus::GetStatus 方法大体相同，不同之处在于如果中止对数据源对象的初始化，前者将返回 E_UNEXPECTED，而不是 DB_E_CANCELED（但是 ISSAsynchStatus::WaitForAsynchCompletion 将返回 DB_E_CANCELED）。 这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另请参阅  
 [接口&#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)    
 [执行异步操作](../../oledb/features/performing-asynchronous-operations.md)  
  
  
