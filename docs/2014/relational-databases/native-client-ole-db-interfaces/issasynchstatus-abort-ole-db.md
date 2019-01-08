---
title: 'Issasynchstatus:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- ISSAsynchStatus::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b61f5e3e44f9584fc3f93efb521585e3173b6c1d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52532047"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
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
  
 取消 DBASYNCHOP_OPEN 请求适用于异步打开或填充行集或数据源对象的异步初始化。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 已处理取消异步操作的请求。 这并不保证操作本身已取消。 若要确定操作是否已取消，使用者应当调用 [ISSAsynchStatus::GetStatus](issasynchstatus-getstatus-ole-db.md)，并检查是否有 DB_E_CANCELED；但是，它可能不会正好在下一次调用中返回。  
  
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
  
## <a name="remarks"></a>备注  
 中止行集或数据源对象的初始化可能使行集或数据源对象最后处于僵停状态，以至于除了 IUnknown 方法以外的所有方法都返回 E_UNEXPECTED。 发生这种情况时，使用者的唯一可能操作是释放行集或数据源对象。  
  
 如果调用 ISSAsynchStatus::Abort 并为 eOperation 传递除了 DBASYNCHOP_OPEN 以外的值，将返回 S_OK。 这并不意味着操作已完成或取消。  
  
## <a name="see-also"></a>请参阅  
 [执行异步操作](../native-client/features/performing-asynchronous-operations.md)  
  
  
