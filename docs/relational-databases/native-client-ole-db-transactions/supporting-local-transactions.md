---
title: 支持本地事务 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8533747bbe5ccb79a06b10a754c4af45ab241843
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280104"
---
# <a name="supporting-local-transactions"></a>支持本地事务
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  会话分隔[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序本地事务的事务范围。 当在使用者的指示下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序向 连接的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例提交请求时，请求构成了[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序的工作单元。 本地事务始终在单个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序会话上包装一个或多个工作单元。  
  
 使用默认[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE DB 提供程序自动提交模式，单个工作单元将被视为本地事务的范围。 只能有一个单元参与本地事务。 创建会话时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将开始会话的事务。 在成功完成工作单元之后提交工作。 如果失败，则回滚任何已开始的任何工作，并向使用者报告错误。 在这两种情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序都启动会话的新本地事务，以便所有工作在事务中执行。  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序使用者可以使用**ITransactionLocal**接口更精确地控制本地事务范围。 当使用者会话启动事务时，事务起点和最终 Commit 或 Abort 方法调用之间的所有会话工作单元都被视为原子单元********。 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序在使用者指示时隐式启动事务。 如果使用者未请求保持，该会话恢复为父事务级行为，通常为自动提交模式。  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序支持**I事务本地：：启动事务**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|** isoLevel[in]|用于该事务的隔离级别。 在本地事务中，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序支持以下内容：<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 注意：从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 开始，ISOLATIONLEVEL_SNAPSHOT 对 isoLevel 参数有效，而不管是否对数据库启用了版本支持**。 但是，如果用户尝试执行语句，并且未启用版本支持和/或数据库不为只读，则将发生错误。 此外，如果在连接到 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以前的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本时将 ISOLATIONLEVEL_SNAPSHOT 指定为 isoLevel，将发生 XACT_E_ISOLATIONLEVEL 错误**。|  
|** isoFlags[in]|本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序返回除零以外的任何值的错误。|  
|** pOtherOptions[in]|如果不是 NULL，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将从接口请求选项对象。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项对象的*ulTimeout*成员不是零，则本机客户端 OLE DB 提供程序将返回XACT_E_NOTIMEOUT。 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序忽略*sz 描述*成员的值。|  
|** pulTransactionLevel[out]|如果不是 NULL，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将返回事务的嵌套级别。|  
  
 对于本地事务，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序实现**I事务：：：中止**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|** pboidReason[in]|忽略（如果设置）。 可以安全地为 NULL。|  
|** fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 FALSE 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将恢复为会话的自动提交模式。|  
|** fAsync[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序不支持异步中止。 如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]值不是 FALSE，本机客户端 OLE 数据库提供程序将返回XACT_E_NOTSUPPORTED。|  
  
 对于本地事务，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序实现**I事务：：提交**参数，如下所示。  
  
|参数|描述|  
|---------------|-----------------|  
|** fRetaining[in]|当该参数为 TRUE 时，将针对会话隐式开始新的事务。 事务必须由使用者提交或中止。 FALSE 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序将恢复为会话的自动提交模式。|  
|** grfTC[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 OLE 数据库提供程序不支持异步和阶段一返回。 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序返回XACT_E_NOTSUPPORTEDXACTTC_SYNC以外的任何值。|  
|** grfRM[in]|必须为 0。|  
  
 会话[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的本机客户端 OLE DB 提供程序行集将保留在本地提交或中止操作上，具体取决于排集属性DBPROP_ABORTPRESERVE和DBPROP_COMMITPRESERVE的值。 默认情况下，这些属性都是VARIANT_FALSE，并且会话上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的所有本机客户端 OLE DB 提供程序行集在中止或提交操作后都会丢失。  
  
 本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序不实现**I事务对象**接口。 尝试检索接口上的引用的使用者将返回 E_NOINTERFACE。  
  
 此示例使用 ITransactionLocal****。  
  
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
 [交易](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [使用快照隔离](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
