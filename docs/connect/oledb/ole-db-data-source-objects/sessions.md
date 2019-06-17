---
title: 会话 |Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序中的会话
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: a2768acd897d996ec3076864a0586be74f22dbdf
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/07/2019
ms.locfileid: "66768438"
---
# <a name="sessions"></a>会话
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server 会话的 OLE DB 驱动程序表示的实例的单个连接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
 SQL Server 的 OLE DB 驱动程序要求会话分隔数据源的事务空间。 通过某一特定会话对象创建的所有命令对象均参与该会话对象的本地事务或分布式事务。  
  
 在已初始化数据源上创建的第一个会话对象接收在初始化期间建立的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接。 当释放该会话对象的接口上的所有引用时，在该数据源上创建的其他会话对象即可使用与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的连接。  
  
 在数据源上创建的其他会话对象建立其自身到该数据源指定的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的连接。 当应用程序释放对创建该会话的对象的所有引用时，将删除与 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的连接。  
  
 下面的示例演示如何使用 SQL Server 的 OLE DB 驱动程序连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库：  
  
```  
int main()  
{  
    // Interfaces used in the example.  
    IDBInitialize*      pIDBInitialize      = NULL;  
    IDBCreateSession*   pIDBCreateSession   = NULL;  
    IDBCreateCommand*   pICreateCmd1        = NULL;  
    IDBCreateCommand*   pICreateCmd2        = NULL;  
    IDBCreateCommand*   pICreateCmd3        = NULL;  
  
    // Initialize COM.  
    if (FAILED(CoInitialize(NULL)))  
    {  
        // Display error from CoInitialize.  
        return (-1);  
    }  
  
    // Get the memory allocator for this task.  
    if (FAILED(CoGetMalloc(MEMCTX_TASK, &g_pIMalloc)))  
    {  
        // Display error from CoGetMalloc.  
        goto EXIT;  
    }  
  
    // Create an instance of the data source object.  
    if (FAILED(CoCreateInstance(CLSID_MSOLEDBSQL, NULL,  
        CLSCTX_INPROC_SERVER, IID_IDBInitialize, (void**)  
        &pIDBInitialize)))  
    {  
        // Display error from CoCreateInstance.  
        goto EXIT;  
    }  
  
    // The InitFromPersistedDS function   
    // performs IDBInitialize->Initialize() establishing  
    // the first application connection to the instance of SQL Server.  
    if (FAILED(InitFromPersistedDS(pIDBInitialize, L"MyDataSource",  
        NULL, NULL)))  
    {  
        goto EXIT;  
    }  
  
    // The IDBCreateSession interface is implemented on the data source  
    // object. Maintaining the reference received maintains the   
    // connection of the data source to the instance of SQL Server.  
    if (FAILED(pIDBInitialize->QueryInterface(IID_IDBCreateSession,  
        (void**) &pIDBCreateSession)))  
    {  
        // Display error from pIDBInitialize.  
        goto EXIT;  
    }  
  
    // Releasing this has no effect on the SQL Server connection  
    // of the data source object because of the reference maintained by  
    // pIDBCreateSession.  
    pIDBInitialize->Release();  
    pIDBInitialize = NULL;  
  
    // The session created next receives the SQL Server connection of  
    // the data source object. No new connection is established.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd1)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // A new connection to the instance of SQL Server is established to support the  
    // next session object created. On successful completion, the  
    // application has two active connections on the SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd2)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
    // pICreateCmd1 has the data source connection. Because the  
    // reference on the IDBCreateSession interface of the data source  
    // has not been released, releasing the reference on the session  
    // object does not terminate a connection to the instance of SQL Server.  
    // However, the connection of the data source object is now   
    // available to another session object. After a successful call to   
    // Release, the application still has two active connections to the   
    // instance of SQL Server.  
    pICreateCmd1->Release();  
    pICreateCmd1 = NULL;  
  
    // The next session created gets the SQL Server connection  
    // of the data source object. The application has two active  
    // connections to the instance of SQL Server.  
    if (FAILED(pIDBCreateSession->CreateSession(NULL,  
        IID_IDBCreateCommand, (IUnknown**) &pICreateCmd3)))  
    {  
        // Display error from pIDBCreateSession.  
        goto EXIT;  
    }  
  
EXIT:  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd1 has the connection of the data source   
    // object.  
    if (pICreateCmd1 != NULL)  
        pICreateCmd1->Release();  
  
    // Releasing the reference on pICreateCmd2 terminates the SQL  
    // Server connection supporting the session object. The application  
    // now has only a single active connection on the instance of SQL Server.  
    if (pICreateCmd2 != NULL)  
        pICreateCmd2->Release();  
  
    // Even on error, this does not terminate a SQL Server connection   
    // because pICreateCmd3 has the connection of the   
    // data source object.  
    if (pICreateCmd3 != NULL)  
        pICreateCmd3->Release();  
  
    // On release of the last reference on a data source interface, the  
    // connection of the data source object to the instance of SQL Server is broken.  
    // The example application now has no SQL Server connections active.  
    if (pIDBCreateSession != NULL)  
        pIDBCreateSession->Release();  
  
    // Called only if an error occurred while attempting to get a   
    // reference on the IDBCreateSession interface of the data source.  
    // If so, the call to IDBInitialize::Uninitialize terminates the   
    // connection of the data source object to the instance of SQL Server.  
    if (pIDBInitialize != NULL)  
    {  
        if (FAILED(pIDBInitialize->Uninitialize()))  
        {  
            // Uninitialize is not required, but it fails if an  
            // interface has not been released. Use it for  
            // debugging.  
        }  
        pIDBInitialize->Release();  
    }  
  
    if (g_pIMalloc != NULL)  
        g_pIMalloc->Release();  
  
    CoUninitialize();  
  
    return (0);  
}  
```  
  
 对于持续创建和释放会话对象的应用程序，连接针对 SQL Server 会话对象的 OLE DB 驱动程序和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例可能会产生很大的开销。 可以通过有效地管理用于 SQL Server 会话对象的 OLE DB 驱动程序降到最低开销。 通过维护至少一个会话对象接口的引用，适用于 SQL Server 应用程序的 OLE DB 驱动程序可以使该对象的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 连接处于活动状态。  
  
 例如，维护命令创建对象引用池将保持该池中这些会话对象的活动连接。 由于需要会话对象，因此，池维护代码将向需要会话的应用程序方法传递有效的 IDBCreateCommand  接口指针。 当应用程序方法不再需要该会话时，该方法将接口指针返回到池维护代码，而不是释放应用程序对命令创建对象的引用。  
  
> [!NOTE]  
>  在前面的示例中，使用 IDBCreateCommand  接口的原因在于 ICommand  接口实现 GetDBSession  方法，该方法是命令或行集作用域中允许对象确定创建其会话的唯一方法。 因此，只有命令对象才允许应用程序检索可创建其他会话的数据源对象指针。  
  
## <a name="see-also"></a>另请参阅  
 [数据源对象&#40;OLE DB&#41;](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
