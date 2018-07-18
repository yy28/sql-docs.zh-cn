---
title: ISSAsynchStatus::WaitForAsynchCompletion (OLE DB) |Microsoft 文档
description: ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
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
- ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
apitype: COM
helpviewer_keywords:
- WaitForAsynchCompletion method
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 7279c4ca68ddf57824a68cb803cbc5d566ad14b4
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689200"
---
# <a name="issasynchstatuswaitforasynchcompletion-ole-db"></a>ISSAsynchStatus::WaitForAsynchCompletion (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

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
 行集是在未使用的状态，因为**itransaction:: 提交**或**ITransaction::Abort**已调用或其初始化阶段期间取消行集。  
  
 DB_E_CANCELED  
 在行集填充或数据源对象初始化过程已取消异步处理。  
  
 DB_S_ASYNCHRONOUS  
 此操作尚未完成，即使已达到指定的超时值。  
  
> [!NOTE]  
>  除了上面列出的返回代码值**ISSAsynchStatus::WaitForAsynchCompletion**方法还支持核心 OLEDB 返回的返回代码值**ICommand::Execute**和**Idbinitialize:: Initialize**方法。  
  
## <a name="remarks"></a>Remarks  
 **ISSAsynchStatus::WaitForAsynchCompletion**方法不会返回之前经过的超时值 （以毫秒为单位） 或完成挂起的操作。 **命令**对象具有**CommandTimeout**属性，用于控制的秒数在超时前将运行查询。**CommandTimeout**属性将被忽略，如果与结合使用**ISSAsynchStatus::WaitForAsynchCompletion**方法。  
  
 对于异步操作，将忽略超时属性。 超时参数**ISSAsynchStatus::WaitForAsynchCompletion**指定的最大控制权返回给调用方之前将等待的时间量。 如果此超时值已到期，将返回 DB_S_ASYNCHRONOUS。 超时从不会取消异步操作。 如果应用程序需要取消在超时期限内未完成的异步操作，则它必须等待发生超时，然后，如果返回 DB_S_ASYNCHRONOUS，则显式取消此操作。  
  
> [!NOTE]  
>  使用 OLE DB 服务组件时，则为 S_OK 时，可能会返回 DB_S_ASYNCHRONOUS 预期行为，因此应用程序应调用[ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md)返回，则为 S_OK 或 DB_S_ASYNCHRONOUS 时检查完成。  
  
 如果*dwMillisecTimeOut*值设置为无限， **ISSAsynchStatus::WaitForAsynchCompletion**方法阻止，直到完成该操作。 如果*dwMillisecTimeOut*值设置为 0，则该方法将立即返回状态为挂起的操作。 如果在超时到期之前完成该操作后，将返回 DB_S_ASYNCHRONOUS。  
  
 如果操作在超时值到期之前完成，则返回的 HRESULT 将为由此操作返回的 HRESULT（如果此操作已以异步方式执行，则应已返回 HRESULT）。  
  
 此外，SSPROP_ISSAsynchStatus 属性已添加到 DBPROPSET_SQLSERVERROWSET 属性集。 支持的提供程序[ISSAsynchStatus](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)接口必须实现此属性与值为 VARIANT_TRUE。  
  
## <a name="see-also"></a>请参阅  
 [执行异步操作](../../oledb/features/performing-asynchronous-operations.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
