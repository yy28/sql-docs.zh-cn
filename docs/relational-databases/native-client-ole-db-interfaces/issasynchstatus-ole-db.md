---
title: ISSAsynchStatus (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus (OLE DB)
apitype: COM
helpviewer_keywords:
- ISSAsynchStatus interface
ms.assetid: c643f09f-9ccc-4d8b-9243-3cde86c2bd46
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 232df02a18bc69a612f9c5a7ea9cdd8da8c75320
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51655496"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **ISSAsynchStatus**公开支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]异步操作。 这是一个可选接口继承自核心 OLE DB 接口**IDBAsynchStatus**。 除了从 IDBAsynchStatus 继承的 Abort 和 GetStatus 方法外，ISSAsynchStatus 还提供一个新方法，用于在完成异步操作或发生超时前等待。  
  
|方法|Description|  
|------------|-----------------|  
|[Issasynchstatus:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[Issasynchstatus:: Getstatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[Issasynchstatus:: Waitforasynchcompletion &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|一直等待，直到异步执行的操作完成或发生超时。|  
  
## <a name="remarks"></a>备注  
 ISSAsynchStatus::GetStatus 方法的 ISSAsynchStatus 实现与 IDBAsynchStatus::GetStatus 方法大体相同，不同之处在于如果中止对数据源对象的初始化，前者将返回 E_UNEXPECTED，而不是 DB_E_CANCELED（但是 ISSAsynchStatus::WaitForAsynchCompletion 将返回 DB_E_CANCELED）。 这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [执行异步操作](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
