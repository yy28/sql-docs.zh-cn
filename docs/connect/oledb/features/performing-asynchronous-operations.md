---
title: 执行异步操作 |Microsoft 文档
description: SQL server 执行与 OLE DB 驱动程序的异步操作
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- initialization [OLE DB Driver for SQL Server]
- database connections [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], asynchronous operations
- connections [OLE DB Driver for SQL Server]
- asynchronous operations [OLE DB Driver for SQL Server]
- rowsets [SQL Server], initializing
- MSOLEDBSQL, asynchronous operations
- OLE DB Driver for SQL Server, asynchronous operations
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 3ba220d754eb3ebc31a719cb840e93378438e09c
ms.sourcegitcommit: 354ed9c8fac7014adb0d752518a91d8c86cdce81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/14/2018
ms.locfileid: "35612132"
---
# <a name="performing-asynchronous-operations"></a>执行异步操作
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 允许应用程序执行异步数据库操作。 异步处理将使方法能够立即返回，而不会阻塞调用线程。 这使得多线程机制能提供更强大的功能和灵活性，而不需要开发人员显式创建线程或处理同步。 应用程序将在初始化数据库连接时或初始化由执行命令所生成的结果时请求异步处理。  
  
## <a name="opening-and-closing-a-database-connection"></a>打开和关闭数据库连接  
 应用程序设计为以异步方式初始化数据源对象时使用用于 SQL Server 的 OLE DB 驱动程序，可以设置 DBPROP_INIT_ASYNCH 属性，然后调用中的位 DBPROPVAL_ASYNCH_INITIALIZE **idbinitialize:: Initialize**. 当设置此属性时，该提供程序返回立即调用**初始化**使用，则为 S_OK，如果该操作完成后立即或 DB_S_ASYNCHRONOUS，如果初始化继续以异步方式。 应用程序可以查询有关**IDBAsynchStatus**或[ISSAsynchStatus](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)接口上数据源对象，然后调用**IDBAsynchStatus::GetStatus**或[ISSAsynchStatus::WaitForAsynchCompletion](../../oledb/ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md)来获取初始化状态。  
  
 此外，SSPROP_ISSAsynchStatus 属性已添加到 DBPROPSET_SQLSERVERROWSET 属性集。 支持的提供程序**ISSAsynchStatus**接口必须实现此属性与值为 VARIANT_TRUE。  
  
 **IDBAsynchStatus::Abort**或[ISSAsynchStatus::Abort](../../oledb/ole-db-interfaces/issasynchstatus-abort-ole-db.md)可以调用以进行取消异步**初始化**调用。 使用者必须显式请求异步数据源初始化。 否则为**idbinitialize:: Initialize**完全初始化的数据源对象后才返回值。  
  
> [!NOTE]  
>  有关连接池使用的数据源对象不能调用**ISSAsynchStatus**中 SQL Server 的 OLE DB 驱动程序接口。 **ISSAsynchStatus**的共用的数据源对象没有公开的接口。  
>   
>  如果应用程序显式强制游标引擎，使用**IOpenRowset::OpenRowset**和**IMultipleResults::GetResult**将不支持异步处理。  
>   
>  此外，不能调用 （MDAC 2.8) 中的远程处理代理/存根 dll **ISSAsynchStatus** OLE DB 驱动程序中的 SQL Server 的接口。 **ISSAsynchStatus**远程处理功能没有公开的接口。  
>   
>  不支持服务组件**ISSAsynchStatus**。  
  
## <a name="execution-and-rowset-initialization"></a>执行和行集初始化  
 被设计成以异步方式打开由执行命令所生成的结果的应用程序可以设置 DBPROP_ROWSET_ASYNCH 属性中的 DBPROPVAL_ASYNCH_INITIALIZE 位。 当设置此位之前调用时**idbinitialize:: Initialize**， **ICommand::Execute**， **IOpenRowset::OpenRowset**或**IMultipleResults::GetResult**、 *riid*参数必须设置为 IID_IDBAsynchStatus、 IID_ISSAsynchStatus 或 IID_IUnknown。  
  
 方法立即返回，则为 S_OK 如果行集初始化完成立即，或与 DB_S_ASYNCHRONOUS，如果行集将继续以异步方式初始化与*ppRowset*上设置为所请求的接口行集。 对于 OLE DB 驱动程序的 SQL Server，此接口仅可以是**IDBAsynchStatus**或**ISSAsynchStatus**。 直到完全初始化的行集时，此接口的行为就像它是在挂起的状态，并调用**QueryInterface**以外的其他接口**IID_IDBAsynchStatus**或**IID_ISSAsynchStatus**可能会返回 E_NOINTERFACE。 除非使用者显式请求异步处理，否则行集将以同步方式执行初始化。 所有请求时，接口将可用**IDBAsynchStaus::GetStatus**或**ISSAsynchStatus::WaitForAsynchCompletion**返回异步操作已完成的指示。 这不一定意味着行集已完全填充，但它是完整的，且功能齐全。  
  
 如果在执行的命令不返回行集，它仍立即返回支持的对象**IDBAsynchStatus**。  
  
 如果需要获得由异步命令执行所产生的多个结果，则应当：  
  
-   在执行命令之前，设置 DBPROP_ROWSET_ASYNCH 属性的 DBPROPVAL_ASYNCH_INITIALIZE 位。  
  
-   调用**ICommand::Execute**，和请求**IMultipleResults**。  
  
 **IDBAsynchStatus**和**ISSAsynchStatus**接口然后可通过查询多个结果接口使用**QueryInterface**。  
  
 当此命令已完成执行， **IMultipleResults**可用作正常，并且从同步的情况下的一个例外： 可以返回 DB_S_ASYNCHRONOUS，在这种情况下**IDBAsynchStatus**或**ISSAsynchStatus**可以用于确定何时完成该操作。  
  
## <a name="examples"></a>示例  
 在以下示例中，应用程序调用非阻止方法，执行一些其他处理，然后返回以处理结果。 **ISSAsynchStatus::WaitForAsynchCompletion**内部事件对象，直到完成异步执行的操作或指定的时间量上等待*dwMilisecTimeOut*被传递。  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
  
DBPROPSET CmdPropset[1];  
DBPROP CmdProperties[1];  
  
CmdPropset[0].rgProperties = CmdProperties;  
CmdPropset[0].cProperties = 1;  
CmdPropset[0].guidPropertySet = DBPROPSET_ROWSET;  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
CmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
  
hr = pICommandProps->SetProperties(1, CmdPropset);  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if ( hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 **ISSAsynchStatus::WaitForAsynchCompletion**内部事件对象上等待，直到完成该以异步方式执行的操作或*dwMilisecTimeOut*传递值。  
  
 以下示例显示有多个结果集的异步处理：  
  
```  
DBPROP CmdProperties[1];  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_IMultipleResults,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pIMultipleResults);  
  
// Use GetResults for ISSAsynchStatus.  
hr = pIMultipleResults->GetResult(IID_ISSAsynchStatus, (void **) &pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if (hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 若要阻止阻塞，客户端可以检查异步操作的运行状态，如以下示例所示：  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);   
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   do{  
      // Do some work...  
      hr = pISSAsynchStatus->GetStatus(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN, NULL, NULL, &ulAsynchPhase, NULL);  
   }while (DBASYNCHPHASE_COMPLETE != ulAsynchPhase)  
   if SUCCEEDED(hr)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
   }  
   pIDBAsynchStatus->Release();  
}  
```  
  
 以下示例演示如何才能取消当前正在运行的异步操作：  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work...  
   hr = pISSAsynchStatus->Abort(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN);  
}  
```  
  
## <a name="see-also"></a>请参阅  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [行集属性和行为](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
