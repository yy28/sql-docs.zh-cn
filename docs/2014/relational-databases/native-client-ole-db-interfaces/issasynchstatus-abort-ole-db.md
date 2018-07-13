---
title: 'Issasynchstatus:: Abort (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- ISSAsynchStatus::Abort (OLE DB)
topic_type:
- apiref
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5711cdcdcedb409330ae1b70591d9fe08db961e1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414148"
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
  
 *eOperation*[in]  
 要中止的操作。 其值应为：  
  
 DBASYNCHOP_OPEN — 要取消的请求应用于对行集的异步打开或填充，或应用于对数据源对象的异步初始化。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 已处理取消异步操作的请求。 这并不保证操作本身已取消。 若要确定是否已取消该操作，使用者应调用[issasynchstatus:: Getstatus](issasynchstatus-getstatus-ole-db.md)并检查是否有 DB_E_CANCELED; 但是，它可能不会返回在紧接着的下一个调用中。  
  
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
  
 **Issasynchstatus:: Abort**在其上的数据源对象上调用**idbinitialize:: Initialize**但随后之前已取消初始化或已超时。数据源对象仍未初始化。  
  
 **Issasynchstatus:: Abort**在其上一个行集合上调用**itransaction:: Commit**或**itransaction:: Abort**以前被调用，并在行集中未提交或中止是处于僵停状态。  
  
 **Issasynchstatus:: Abort**已以异步方式取消初始化阶段中的行集时调用。 该行集处于僵停状态。  
  
## <a name="remarks"></a>Remarks  
 中止行集或数据源对象的初始化可能使行集或数据源对象处于僵停状态，以便所有方法以外的其他**IUnknown**方法将返回 E_UNEXPECTED。 发生这种情况时，使用者的唯一可能操作是释放行集或数据源对象。  
  
 调用**issasynchstatus:: Abort**并将值传递*eOperation*除了 DBASYNCHOP_OPEN 返回 S_OK。 这并不意味着操作已完成或取消。  
  
## <a name="see-also"></a>请参阅  
 [执行异步操作](../native-client/features/performing-asynchronous-operations.md)  
  
  
