---
title: ISSAsynchStatus::Abort (OLE DB) |Microsoft 文档
description: ISSAsynchStatus::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f4070ab6a99a809fa0486dfd9462431e5608d25
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  取消异步执行的操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>参数  
 *hChapter*[in]  
 要中止其操作的章节的句柄。 如果被调用的对象不是行集对象或操作不能应用于一章，调用方必须设置*hChapter*到 DB_NULL_HCHAPTER。  
  
 *eOperation*[in]  
 要中止的操作。 应使用以下值：  
  
 DBASYNCHOP_OPEN — 要取消的请求应用于对行集的异步打开或填充，或应用于对数据源对象的异步初始化。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 已处理取消异步操作的请求。 它不保证操作本身已取消。 若要确定是否已取消该操作，使用者应调用[ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)并检查 DB_E_CANCELED; 但是，它可能不会返回非常下一个调用中。  
  
 DB_E_CANTCANCEL  
 异步操作无法取消。  
  
 DB_E_CANCELED  
 中止异步操作的请求已在通知期间取消。 操作仍然正在异步执行。  
  
 E_FAIL  
 发生了特定于访问接口的错误。  
  
 E_INVALIDARG  
 *HChapter*参数不 DB_NULL_HCHAPTER 或*eOperation*不 DBASYNCH_OPEN。  
  
 E_UNEXPECTED  
 **ISSAsynchStatus::Abort**对数据源对象在其上调用了**idbinitialize:: Initialize**尚未被调用，或尚未完成。  
  
 **ISSAsynchStatus::Abort**对数据源对象在其上调用了**idbinitialize:: Initialize**随后之前已取消初始化，但调用时或超时为止。数据源对象仍未初始化。  
  
 **ISSAsynchStatus::Abort**对在其上的行集调用**itransaction:: 提交**或**ITransaction::Abort**之前已调用和行集没有幸存提交或中止，处于僵停状态。  
  
 **ISSAsynchStatus::Abort**已以异步方式取消其初始化阶段中的行集调用的。 该行集处于僵停状态。  
  
## <a name="remarks"></a>注释  
 正在中止行集或数据源对象的初始化可能导致行集或数据源对象处于僵停状态，以便以外的其他所有方法**IUnknown**方法返回 E_UNEXPECTED。 发生这种情况时，使用者的唯一可能操作是释放行集或数据源对象。  
  
 调用**ISSAsynchStatus::Abort**和传递一个值*eOperation*之外 DBASYNCHOP_OPEN 返回，则为 S_OK。 这并不意味着该操作完成或已取消。  
  
## <a name="see-also"></a>另请参阅  
 [执行异步操作](../../oledb/features/performing-asynchronous-operations.md)  
  
  
