---
title: 支持本地事务 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b75104940cca183005f8a465ea19d0a517247c25
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213816"
---
# <a name="supporting-local-transactions"></a>支持本地事务
  会话分隔的事务范围[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口本地事务。 当使用者，指示[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序将请求提交到连接的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，该请求构成的工作单位[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 本地事务始终将一个或多个工作单元包装对单个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口会话。  
  
 使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口自动提交模式下，单个工作单元视为本地事务的作用域。 只能有一个单元参与本地事务。 创建会话， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口开始会话的事务。 在成功完成工作单元之后提交工作。 如果失败，则回滚任何已开始的任何工作，并向使用者报告错误。 在任一情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口开始会话的新本地事务，以便在一个事务内执行所有工作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口使用者可以通过使用直接更加精确地控制本地事务范围**ITransactionLocal**接口。 当使用者会话启动事务时，事务起点和最终 Commit 或 Abort 方法调用之间的所有会话工作单元都被视为原子单元。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序隐式开始一个事务时执行此操作由使用者。 如果使用者未请求保持，该会话恢复为父事务级行为，通常为自动提交模式。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口支持**itransactionlocal:: Starttransaction**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|isoLevel[in]|用于该事务的隔离级别。 本地事务中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序支持以下各项：<br /><br /> -ISOLATIONLEVEL_UNSPECIFIED<br />-ISOLATIONLEVEL_CHAOS<br />-   ISOLATIONLEVEL_READUNCOMMITTED<br />-   ISOLATIONLEVEL_READCOMMITTED<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-ISOLATIONLEVEL_CURSORSTABILITY<br />-   ISOLATIONLEVEL_REPEATABLEREAD<br />-   ISOLATIONLEVEL_SERIALIZABLE<br />-ISOLATIONLEVEL_ISOLATED<br />-ISOLATIONLEVEL_SNAPSHOT**注意：** 开头[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，ISOLATIONLEVEL_SNAPSHOT 无效*isoLevel*参数是否为数据库启用版本控制。 但是，如果用户尝试执行语句，并且未启用版本支持和/或数据库不为只读，则将发生错误。 此外，如果在连接到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本时将 ISOLATIONLEVEL_SNAPSHOT 指定为 isoLevel，将发生 XACT_E_ISOLATIONLEVEL 错误。|  
|isoFlags[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将返回错误的任何非零值。|  
|pOtherOptions[in]|如果不为 NULL， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口从接口请求选项对象。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口返回 XACT_E_NOTIMEOUT 如果选项对象*ulTimeout*成员不为零。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将忽略的值*szDescription*成员。|  
|pulTransactionLevel[out]|如果不为 NULL， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口将返回事务的嵌套的级别。|  
  
 对于本地事务， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口实现**itransaction:: Abort**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|pboidReason[in]|忽略（如果设置）。 可以安全地为 NULL。|  
|fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序为该会话将恢复为自动提交模式。|  
|fAsync[in]|不支持异步中止[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口返回 XACT_E_NOTSUPPORTED，如果值不是 FALSE。|  
  
 对于本地事务， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口实现**itransaction:: Commit**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 为 FALSE 时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序为该会话将恢复为自动提交模式。|  
|grfTC[in]|不支持异步和一个返回的阶段[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口为 XACTTC_SYNC 以外的任何值返回 XACT_E_NOTSUPPORTED。|  
|grfRM[in]|必须为 0。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口行集对该会话将保留在本地提交或中止操作的行集属性 DBPROP_ABORTPRESERVE 和 DBPROP_COMMITPRESERVE 的值。 默认情况下，这些属性是 VARIANT_FALSE 及其所有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口行集对该会话将都会丢失以下中止或提交操作。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口不实现**ITransactionObject**接口。 尝试检索接口上的引用的使用者将返回 E_NOINTERFACE。  
  
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
  
## <a name="see-also"></a>请参阅  
 [事务](transactions.md)   
 [使用快照隔离](../native-client/features/working-with-snapshot-isolation.md)  
  
  
