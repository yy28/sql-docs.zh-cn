---
title: 支持分布式的事务 |Microsoft 文档
description: SQL Server 的 OLE DB 驱动程序中的分布式的事务
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8e738e8bb125350d8d4aec91317495fc4c1fa489
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="supporting-distributed-transactions"></a>支持分布式事务
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 驱动程序的 SQL Server 使用者可以使用**ITransactionJoin::JoinTransaction**方法可以参与分布式事务协调由 Microsoft 分布式事务处理协调器 (MS DTC)。  
  
 MS DTC 公开 COM 对象，这些对象允许客户端跨各种数据存储的多个连接来启动和参与协调的事务。 若要启动事务，OLE DB 驱动程序的 SQL Server 使用者使用 MS DTC **ITransactionDispenser**接口。 **BeginTransaction**的成员**ITransactionDispenser**分布式的事务对象上返回的引用。 此引用传递给 OLE DB 驱动程序的 SQL Server 使用**JoinTransaction**。  
  
 MS DTC 支持对分布式事务的异步提交和中止。 对于异步事务状态的通知，使用者实现**ITransactionOutcomeEvents**接口，并连接到的 MS DTC 事务对象的接口。  
  
 对于分布式事务，SQL Server 的 OLE DB 驱动程序实现**ITransactionJoin::JoinTransaction** ，如下所示的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|*punkTransactionCoord*|指向 MS DTC 事务对象的指针。|  
|*IsoLevel*|适用于 SQL Server 忽略 OLE DB 驱动程序。 使用者在从 MS DTC 获取事务对象时，确定由 MS DTC 协调的事务的隔离级别。|  
|*IsoFlags*|必须为 0。 SQL Server 的 OLE DB 驱动程序返回 XACT_E_NOISORETAIN，如果由使用者指定任何其他值。|  
|*POtherOptions*|如果不是 NULL、 SQL Server 的 OLE DB 驱动程序从界面请求选项对象。 如果 SQL Server 的 OLE DB 驱动程序返回 XACT_E_NOTIMEOUT 选项对象的*ulTimeout*成员不为零。 SQL Server 的 OLE DB 驱动程序将忽略的值*szDescription*成员。|  
  
 下面的示例通过使用 MS DTC 来协调事务：  
  
```  
// Interfaces used in the example.  
IDBCreateSession*       pIDBCreateSession   = NULL;  
ITransactionJoin*       pITransactionJoin   = NULL;  
IDBCreateCommand*       pIDBCreateCommand   = NULL;  
IRowset*                pIRowset            = NULL;  
  
// Transaction dispenser and transaction from MS DTC.  
ITransactionDispenser*  pITransactionDispenser = NULL;  
ITransaction*           pITransaction       = NULL;  
  
    HRESULT             hr;  
  
// Get the command creation interface for the session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
// Get a transaction dispenser object from MS DTC and  
// start a transaction.  
if (FAILED(hr = DtcGetTransactionManager(NULL, NULL,  
    IID_ITransactionDispenser, 0, 0, NULL,  
    (void**) &pITransactionDispenser)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
if (FAILED(hr = pITransactionDispenser->BeginTransaction(  
    NULL, ISOLATIONLEVEL_READCOMMITTED, ISOFLAG_RETAIN_DONTCARE,  
    NULL, &pITransaction)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
  
// Join the transaction.  
if (FAILED(pIDBCreateCommand->QueryInterface(IID_ITransactionJoin,  
    (void**) &pITransactionJoin)))  
    {  
    // Process failure to get an interface, release any references, and  
    // then return.  
    }  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) pITransaction, 0, 0, NULL)))  
    {  
    // Process join failure, release any references, and then return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then abort.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, 0, 0)))  
        {  
        // Get error from failed commit.  
        //  
        // If a distributed commit fails, application logic could  
        // analyze failure and retry. In this example, terminate. The   
        // consumer must resolve this somehow.  
        pITransaction->Abort(NULL, FALSE, FALSE);  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Un-enlist from the distributed transaction by setting   
// the transaction object pointer to NULL.  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) NULL, 0, 0, NULL)))  
    {  
    // Process failure, and then return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>另请参阅  
 [事务](../../oledb/ole-db-transactions/transactions.md)  
  
  
