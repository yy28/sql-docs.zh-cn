---
title: ISSAsynchStatus (OLE DB) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2c6bc2d66be0b89a62b5b1c678a955891cc06c4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306705"
---
# <a name="issasynchstatus-ole-db"></a>ISSAsynchStatus (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **ISSAsynchStatus**公开了对[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]异步操作的支持。 这是从核心 OLE DB 接口**IDBAsynchStatus**继承的可选接口。 除了从 IDBAsynchStatus 继承的 Abort 和 GetStatus 方法外，ISSAsynchStatus 还提供一个新方法，用于在完成异步操作或发生超时前等待****************。  
  
|方法|描述|  
|------------|-----------------|  
|[ISSAsynchStatus::Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)|取消异步执行的操作。|  
|[ISSAsynchStatus::GetStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)|返回异步执行操作的状态。|  
|[ISSAsynchStatus::WaitForAsynchCompletion &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)|一直等待，直到异步执行的操作完成或发生超时。|  
  
## <a name="remarks"></a>备注  
 ISSAsynchStatus::GetStatus 方法的 ISSAsynchStatus 实现与 IDBAsynchStatus::GetStatus 方法大体相同，不同之处在于如果中止对数据源对象的初始化，前者将返回 E_UNEXPECTED，而不是 DB_E_CANCELED（但是 ISSAsynchStatus::WaitForAsynchCompletion 将返回 DB_E_CANCELED）****************。 这是因为在中止操作后，数据源对象不会仍处于常态，以便进一步尝试初始化操作。  
  
 以下方法支持在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中执行异步操作：  
  
-   **ICommand::Execute**  
  
-   **IOpenRowset::OpenRowset**  
  
-   **IMultipleResults::GetResult**  
  
## <a name="see-also"></a>另请参阅  
 [&#40;OLE DB&#41;的接口](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [执行异步操作](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
