---
title: 支持本地事务 |Microsoft Docs
description: OLE DB Driver for SQL Server 中的本地事务
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: c0cfc1ad6ff3439efe458f97394909c919b77075
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993959"
---
# <a name="supporting-local-transactions"></a>支持本地事务
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  会话分隔 SQL Server 本地事务的 OLE DB 驱动程序的事务作用域。 当使用者的方向, SQL Server 的 OLE DB 驱动程序将请求提交到连接的[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]实例, 则该请求构成用于 SQL Server 的 OLE DB 驱动程序的工作单元。 本地事务始终在 SQL Server 会话的单个 OLE DB 驱动程序上包装一个或多个工作单元。  
  
 使用默认的适用于 SQL Server 的 OLE DB 驱动程序自动提交模式，将一个工作单元视为本地事务的范围。 只能有一个单元参与本地事务。 当创建会话时, SQL Server 的 OLE DB 驱动程序将为会话启动一个事务。 在成功完成工作单元之后提交工作。 如果失败，则回滚任何已开始的任何工作，并向使用者报告错误。 无论哪种情况，适用于 SQL Server 的 OLE DB 驱动程序都会为会话开始新的本地事务，以便在一个事务中执行所有工作。  
  
 适用于 SQL Server 的 OLE DB 驱动程序使用者可使用 ITransactionLocal 接口对本地事务范围进行更精确的控制  。 当使用者会话启动事务时，事务起点和最终 Commit 或 Abort 方法调用之间的所有会话工作单元都被视为原子单元   。 当使用者指示 SQL Server 的 OLE DB 驱动程序时, 它会隐式启动事务。 如果使用者未请求保持，该会话恢复为父事务级行为，通常为自动提交模式。  
  
 SQL Server 的 OLE DB 驱动程序支持**ITransactionLocal:: StartTransaction**参数, 如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
| isoLevel[in]|用于该事务的隔离级别。 在本地事务中, SQL Server 的 OLE DB 驱动程序支持以下各项:<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意：从 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 开始，ISOLATIONLEVEL_SNAPSHOT 对 isoLevel 参数有效，而不管是否对数据库启用了版本支持  。 但是，如果用户尝试执行语句，并且未启用版本支持和/或数据库不为只读，则将发生错误。 此外，如果在连接到 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 以前的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 版本时将 ISOLATIONLEVEL_SNAPSHOT 指定为 isoLevel，将发生 XACT_E_ISOLATIONLEVEL 错误  。|  
| isoFlags[in]|对于任何非零值, SQL Server 的 OLE DB 驱动程序将返回错误。|  
| pOtherOptions[in]|如果不为 NULL, 则 SQL Server 的 OLE DB 驱动程序从接口请求选项对象。 如果选项对象的*ulTimeout*成员不为零, 则 SQL Server 的 OLE DB 驱动程序将返回 XACT_E_NOTIMEOUT。 SQL Server 的 OLE DB 驱动程序将忽略*szDescription*成员的值。|  
| pulTransactionLevel[out]|如果不为 NULL, 则 SQL Server 的 OLE DB 驱动程序将返回事务的嵌套级别。|  
  
 对于本地事务, SQL Server 的 OLE DB 驱动程序实现**ITransaction:: Abort**参数, 如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
| pboidReason[in]|忽略（如果设置）。 可以安全地为 NULL。|  
| fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时, SQL Server 的 OLE DB 驱动程序恢复会话的自动提交模式。|  
| fAsync[in]|SQL Server 的 OLE DB 驱动程序不支持异步中止。 如果值不为 FALSE, 则 SQL Server 的 OLE DB 驱动程序将返回 XACT_E_NOTSUPPORTED。|  
  
 对于本地事务, SQL Server 的 OLE DB 驱动程序实现**ITransaction:: Commit**参数, 如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
| fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时, SQL Server 的 OLE DB 驱动程序恢复会话的自动提交模式。|  
| grfTC[in]|SQL Server 的 OLE DB 驱动程序不支持异步和阶段的一个返回。 SQL Server 的 OLE DB 驱动程序为除 XACTTC_SYNC 以外的任何值返回 XACT_E_NOTSUPPORTED。|  
| grfRM[in]|必须为 0。|  
  
 会话上的适用于 SQL Server 的 OLE DB 驱动程序行集根据行集属性 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 的值保留在本地提交或中止操作中。 默认情况下，这些属性均为 VARIANT_FALSE，并且在执行中止或提交操作之后，将丢失该会话上的所有适用于 SQL Server 的 OLE DB 驱动程序行集。  
  
 SQL Server 的 OLE DB 驱动程序未实现**ITransactionObject**接口。 尝试检索接口上的引用的使用者将返回 E_NOINTERFACE。  
  
 此示例使用 ITransactionLocal  。  
  
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
  
  
