---
title: 'Issasynchstatus:: Waitforasynchcompletion (OLE DB) |Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
ms.assetid: 9f65e9e7-eb93-47a1-bc42-acd4649fbd0e
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cd159c230fc7a53367c0a05d1b36905635391799
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37427236"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  一直等待，直到异步执行的操作完成或发生超时。  
  
## <a name="syntax"></a>语法  
  
```  
  
HRESULT WaitForAsynchCompletion(   
        DWORD dwMillisecTimeOut);  
```  
  
## <a name="arguments"></a>参数  
 *dwMillisecTimeOut*[in]  
 超时值（毫秒）。  
  
## <a name="return-code-values"></a>返回代码值  
 S_OK  
 方法成功。  
  
 E_UNEXPECTED  
 行集是在未使用状态，因为**itransaction:: Commit**或**itransaction:: Abort**已调用或行集初始化阶段已被取消。  
  
 DB_E_CANCELED  
 异步处理在行集填充或数据源对象初始化过程中被取消。  
  
 DB_S_ASYNCHRONOUS  
 此操作尚未完成，即使已达到指定的超时值。  
  
> [!NOTE]  
>  除了以上所列的返回代码值之外**issasynchstatus:: Waitforasynchcompletion**方法还支持由核心 OLEDB 返回的返回代码值**icommand:: Execute**并**Idbinitialize:: Initialize**方法。  
  
## <a name="remarks"></a>Remarks  
 **Issasynchstatus:: Waitforasynchcompletion**方法不会返回之前经过的超时值 （以毫秒为单位） 或完成挂起操作。 **命令**对象具有**CommandTimeout**属性，用于控制的秒数后才超时将运行查询。**CommandTimeout**属性将被忽略，如果结合使用**issasynchstatus:: Waitforasynchcompletion**方法。  
  
 对于异步操作，将忽略超时属性。 超时参数**issasynchstatus:: Waitforasynchcompletion**指定的最大控制权返回给调用方之前经过的时间量。 如果此超时值已到期，将返回 DB_S_ASYNCHRONOUS。 超时从不会取消异步操作。 如果应用程序需要取消在超时期限内未完成的异步操作，则它必须等待发生超时，然后，如果返回 DB_S_ASYNCHRONOUS，则显式取消此操作。  
  
> [!NOTE]  
>  当使用 OLE DB 服务组件时，则为 S_OK 时可能返回 DB_S_ASYNCHRONOUS 预期行为，因此应用程序应调用[issasynchstatus:: Getstatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)返回 S_OK 或 DB_S_ASYNCHRONOUS 时检查完成。  
  
 如果*dwMillisecTimeOut*值设置为 INFINITE， **issasynchstatus:: Waitforasynchcompletion**方法进行阻止，直到操作完成。 如果*dwMillisecTimeOut*值设置为 0，则该方法将立即返回状态为挂起的操作。 如果在完成此操作之前超时值已到期，则将返回 DB_S_ASYNCHRONOUS。  
  
 如果操作在超时值到期之前完成，则返回的 HRESULT 将为由此操作返回的 HRESULT（如果此操作已以异步方式执行，则应已返回 HRESULT）。  
  
 此外，SSPROP_ISSAsynchStatus 属性已添加到 DBPROPSET_SQLSERVERROWSET 属性集。 支持的提供程序[ISSAsynchStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)接口必须实现此属性与值为 VARIANT_TRUE。  
  
## <a name="see-also"></a>请参阅  
 [执行异步操作](../../relational-databases/native-client/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
