---
title: 'Issasynchstatus:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1c903af9545ee65b19a582e7b042c7c05dfb200f
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43079915"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  取消异步执行的操作。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>参数  
 *hChapter*[in]  
 要中止其操作的章节的句柄。 如果所调用的对象不是行集对象或操作不适用于一章，调用方必须设置*hChapter*为 DB_NULL_HCHAPTER。  
  
 eOperation[in]  
 要中止的操作。 其值应为：  
  
 DBASYNCHOP_OPEN — 要取消的请求应用于对行集的异步打开或填充，或应用于对数据源对象的异步初始化。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 已处理取消异步操作的请求。 这并不保证操作本身已取消。 若要确定操作是否已取消，使用者应当调用 [ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)，并检查是否有 DB_E_CANCELED；但是，它可能不会正好在下一次调用中返回。  
  
 DB_E_CANTCANCEL  
 异步操作无法取消。  
  
 DB_E_CANCELED  
 中止异步操作的请求已在通知期间取消。 操作仍然正在异步执行。  
  
 E_FAIL  
 发生了特定于访问接口的错误。  
  
 E_INVALIDARG  
 *HChapter*参数不是 DB_NULL_HCHAPTER 或者*eOperation*不是 DBASYNCH_OPEN。  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Abort**在其上的数据源对象上调用**idbinitialize:: Initialize**尚未调用，或未完成。  
  
 已对数据源对象调用 ISSAsynchStatus::Abort，此前，该对象已调用 IDBInitialize::Initialize 但随后在初始化或超时之前取消。数据源对象仍未初始化。  
  
 **Issasynchstatus:: Abort**在其上一个行集合上调用**itransaction:: Commit**或**itransaction:: Abort**以前被调用，并在行集中未提交或中止是处于僵停状态。  
  
 已对在初始化阶段异步取消的行集调用 ISSAsynchStatus::Abort。 该行集处于僵停状态。  
  
## <a name="remarks"></a>Remarks  
 中止行集或数据源对象的初始化可能使行集或数据源对象最后处于僵停状态，以至于除了 IUnknown 方法以外的所有方法都返回 E_UNEXPECTED。 发生这种情况时，使用者的唯一可能操作是释放行集或数据源对象。  
  
 如果调用 ISSAsynchStatus::Abort 并为 eOperation 传递除了 DBASYNCHOP_OPEN 以外的值，将返回 S_OK。 这并不意味着操作已完成或取消。  
  
## <a name="see-also"></a>请参阅  
 [执行异步操作](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  
