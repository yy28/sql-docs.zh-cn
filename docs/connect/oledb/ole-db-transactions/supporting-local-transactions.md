---
title: 支持本地事务 |Microsoft 文档
description: OLE DB 驱动程序中的 SQL Server 的本地事务
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
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
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 1422292b81c6677ad49bf977e437f6ec4828dc1d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="supporting-local-transactions"></a>支持本地事务
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  会话分隔 SQL Server 本地事务 OLE DB 驱动程序的事务的范围。 SQL Server 的 OLE DB 驱动程序提交到连接的实例的请求时，在使用者的方向， [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]，请求构成的 SQL Server 的 OLE DB 驱动程序的工作单元。 本地事务始终环绕一个或多个工作单元单个 OLE DB 驱动程序为 SQL Server 会话。  
  
 使用默认 OLE DB 驱动程序适用于 SQL Server 自动提交模式，单个工作单元将被视为本地事务的作用域。 只能有一个单元参与本地事务。 创建会话时，SQL Server 的 OLE DB 驱动程序将开始会话的事务。 在成功完成工作单元之后提交工作。 如果失败，则回滚任何已开始的任何工作，并向使用者报告错误。 在任一情况下，SQL Server 的 OLE DB 驱动程序开始会话的新本地事务，以便在事务中执行所有工作。  
  
 OLE DB 驱动程序的 SQL Server 使用者可以通过使用直接更加精确地控制本地事务范围**ITransactionLocal**接口。 当使用者会话启动事务时，事务之间的所有会话工作单元都启动点和最终**提交**或**中止**方法调用被视为一个原子单元。 SQL Server 的 OLE DB 驱动程序隐式开始一项事务作出指示时才为此，使用者。 如果使用者未请求保持，该会话恢复为父事务级行为，通常为自动提交模式。  
  
 SQL Server 的 OLE DB 驱动程序支持**ITransactionLocal::StartTransaction** ，如下所示的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|*isoLevel*[in]|用于该事务的隔离级别。 在本地事务、 SQL Server 的 OLE DB 驱动程序支持以下功能：<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意： 开头[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]，ISOLATIONLEVEL_SNAPSHOT 可用于*isoLevel*自变量是否为数据库启用版本控制。 但是，如果用户尝试执行语句，并且未启用版本支持和/或数据库不为只读，则将发生错误。 此外，将发生错误 XACT_E_ISOLATIONLEVEL，如果 ISOLATIONLEVEL_SNAPSHOT 指定为*isoLevel*连接到的版本时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]早于[!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]。|  
|*isoFlags*[in]|SQL Server 的 OLE DB 驱动程序返回非零的任何值错误。|  
|*pOtherOptions*[in]|如果不是 NULL、 SQL Server 的 OLE DB 驱动程序从界面请求选项对象。 如果 SQL Server 的 OLE DB 驱动程序返回 XACT_E_NOTIMEOUT 选项对象的*ulTimeout*成员不为零。 SQL Server 的 OLE DB 驱动程序将忽略的值*szDescription*成员。|  
|*pulTransactionLevel*[out 一个]|如果不为 NULL、 SQL Server 的 OLE DB 驱动程序返回的事务嵌套的级别。|  
  
 SQL Server 的 OLE DB 驱动程序实现的本地事务**ITransaction::Abort** ，如下所示的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|*pboidReason*[in]|忽略（如果设置）。 可以安全地为 NULL。|  
|*fRetaining*[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时，SQL Server 的 OLE DB 驱动程序将恢复到自动提交模式会话。|  
|*fAsync*[in]|适用于 SQL Server 中，OLE DB 驱动程序不被支持异步中止。 如果该值不是 FALSE，则 SQL Server 的 OLE DB 驱动程序返回 XACT_E_NOTSUPPORTED。|  
  
 SQL Server 的 OLE DB 驱动程序实现的本地事务**itransaction:: 提交**，如下所示的参数。  
  
|参数|Description|  
|---------------|-----------------|  
|*fRetaining*[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时，SQL Server 的 OLE DB 驱动程序将恢复到自动提交模式会话。|  
|*grfTC*[in]|以异步方式和一个返回的阶段不支持通过 OLE DB 驱动程序适用于 SQL Server。 SQL Server 的 OLE DB 驱动程序返回 XACT_E_NOTSUPPORTED XACTTC_SYNC 以外的任何值。|  
|*grfRM*[in]|必须为 0。|  
  
 对该会话的行集保留在本地提交或中止操作的 SQL Server 的 OLE DB 驱动程序 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 基于行集属性的值。 默认情况下，这些属性是 VARIANT_FALSE 和所有 OLE DB 驱动程序的 SQL Server 对该会话的行集将会丢失以下中止或提交操作。  
  
 SQL Server 的 OLE DB 驱动程序不实现**ITransactionObject**接口。 尝试检索接口上的引用的使用者将返回 E_NOINTERFACE。  
  
 此示例使用**ITransactionLocal**。  
  
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
  
  
