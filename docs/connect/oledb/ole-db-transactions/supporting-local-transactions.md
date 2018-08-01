---
title: 支持本地事务 |Microsoft Docs
description: SQL Server 的 OLE DB 驱动程序中本地事务
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8bf157a5f5bdbea93c9361edc4903c5cd6c41302
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109719"
---
# <a name="supporting-local-transactions"></a>支持本地事务
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  会话分隔 OLE DB Driver for SQL Server 本地事务的事务作用的域。 SQL Server 的 OLE DB 驱动程序提交到连接的实例的请求时，在使用者的方向， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，该请求构成的 SQL Server 的 OLE DB 驱动程序的工作单元。 本地事务始终将一个或多个工作单元的单个 OLE DB 驱动程序为 SQL Server 会话。  
  
 使用默认的适用于 SQL Server 的 OLE DB 驱动程序自动提交模式，将一个工作单元视为本地事务的范围。 只能有一个单元参与本地事务。 创建会话时，SQL Server 的 OLE DB 驱动程序将开始会话的事务。 在成功完成工作单元之后提交工作。 如果失败，则回滚任何已开始的任何工作，并向使用者报告错误。 无论哪种情况，适用于 SQL Server 的 OLE DB 驱动程序都会为会话开始新的本地事务，以便在一个事务中执行所有工作。  
  
 适用于 SQL Server 的 OLE DB 驱动程序使用者可使用 ITransactionLocal 接口对本地事务范围进行更精确的控制。 当使用者会话启动事务时，事务起点和最终 Commit 或 Abort 方法调用之间的所有会话工作单元都被视为原子单元。 SQL Server 的 OLE DB 驱动程序隐式开始一个事务时执行此操作由使用者。 如果使用者未请求保持，该会话恢复为父事务级行为，通常为自动提交模式。  
  
 适用于 SQL Server 的 OLE DB 驱动程序支持**itransactionlocal:: Starttransaction**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|isoLevel[in]|用于该事务的隔离级别。 在本地事务中，SQL Server 的 OLE DB 驱动程序支持以下功能：<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意：从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 开始，ISOLATIONLEVEL_SNAPSHOT 对 isoLevel 参数有效，而不管是否对数据库启用了版本支持。 但是，如果用户尝试执行语句，并且未启用版本支持和/或数据库不为只读，则将发生错误。 此外，如果在连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本时将 ISOLATIONLEVEL_SNAPSHOT 指定为 isoLevel，将发生 XACT_E_ISOLATIONLEVEL 错误。|  
|isoFlags[in]|SQL Server 的 OLE DB 驱动程序返回错误的任何非零值。|  
|pOtherOptions[in]|如果不是 NULL，则 SQL Server 的 OLE DB 驱动程序从接口请求选项对象。 SQL Server 的 OLE DB 驱动程序返回 XACT_E_NOTIMEOUT 如果选项对象的*ulTimeout*成员不为零。 SQL Server 的 OLE DB 驱动程序将忽略的值*szDescription*成员。|  
|pulTransactionLevel[out]|如果不为 NULL，则 SQL Server 的 OLE DB 驱动程序返回事务的嵌套的级别。|  
  
 SQL Server 的 OLE DB 驱动程序实现的本地事务**itransaction:: Abort**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|pboidReason[in]|忽略（如果设置）。 可以安全地为 NULL。|  
|fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时，SQL Server 的 OLE DB 驱动程序将恢复为自动提交模式会话。|  
|fAsync[in]|适用于 SQL Server 中，OLE DB 驱动程序不被支持异步中止。 如果值不是 FALSE，则 SQL Server 的 OLE DB 驱动程序返回 XACT_E_NOTSUPPORTED。|  
  
 SQL Server 的 OLE DB 驱动程序实现的本地事务**itransaction:: Commit**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时，SQL Server 的 OLE DB 驱动程序将恢复为自动提交模式会话。|  
|grfTC[in]|异步和一个返回的阶段不支持通过 OLE DB 驱动程序适用于 SQL Server。 SQL Server 的 OLE DB 驱动程序为 XACTTC_SYNC 以外的任何值返回 XACT_E_NOTSUPPORTED。|  
|grfRM[in]|必须为 0。|  
  
 会话上的适用于 SQL Server 的 OLE DB 驱动程序行集根据行集属性 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 的值保留在本地提交或中止操作中。 默认情况下，这些属性均为 VARIANT_FALSE，并且在执行中止或提交操作之后，将丢失该会话上的所有适用于 SQL Server 的 OLE DB 驱动程序行集。  
  
 SQL Server 的 OLE DB 驱动程序不实现**ITransactionObject**接口。 尝试检索接口上的引用的使用者将返回 E_NOINTERFACE。  
  
 此示例使用 ITransactionLocal。  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
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
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>另请参阅  
 [事务](../../oledb/ole-db-transactions/transactions.md)   
 [使用快照隔离](../../oledb/features/working-with-snapshot-isolation.md)  
  
  
