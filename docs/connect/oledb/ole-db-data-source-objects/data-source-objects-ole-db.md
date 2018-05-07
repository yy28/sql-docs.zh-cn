---
title: 数据源对象 (OLE DB) |Microsoft 文档
description: 数据源对象 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], data source objects
- OLE DB Driver for SQL Server, data source objects
- MSOLEDBSQL, data source objects
- OLE DB Driver for SQL Server, data source objects
- OLE DB data source objects [OLE DB Driver for SQL Server]
- data source objects [OLE DB]
- CLSID
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2eb3583366cf896ecf2382a5d2f36d1298e4c4a4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-objects-ole-db"></a>数据源对象 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 驱动程序的 SQL Server 使用术语数据源进行的一套用于如建立到数据存储，链接的 OLE DB 接口[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 创建提供程序的数据源对象的实例是 OLE DB 驱动程序的 SQL Server 使用者的第一个任务。  
  
 每个 OLE DB 访问接口都为自身声明一个类标识符 (CLSID)。 SQL Server 的 OLE DB 驱动程序的 CLSID 是 C/c + + GUID CLSID_MSOLEDBSQL (MSOLEDBSQL_CLSID 将解析为正确的符号 progid 引用 msoledbsql.h 文件中)。 对于 CLSID，使用者使用 OLE **CoCreateInstance**函数制造数据源对象的实例。  
  
 OLE DB 驱动程序的 SQL Server 是一个进程内服务器。 SQL Server 对象的 OLE DB 驱动程序的实例是使用 CLSCTX_INPROC_SERVER 宏以指示可执行上下文创建的。  
  
 为 SQL Server 数据源对象 OLE DB 驱动程序显示允许的使用者连接到现有的 OLE DB 初始化接口[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据库。  
  
 可通过 OLE DB 驱动程序执行 SQL Server 的每个连接将自动设置这些选项：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 此示例使用类标识符宏来创建 OLE DB 驱动程序，SQL Server 数据源对象，并获取对引用其**IDBInitialize**接口。  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER,  
    IID_IDBInitialize, (void**) &pIDBInitialize);  
  
if (SUCCEEDED(hr))  
{  
    //  Perform necessary processing with the interface.  
    pIDBInitialize->Uninitialize();  
    pIDBInitialize->Release();  
}  
else  
{  
    // Display error from CoCreateInstance.  
}  
```  
  
 成功创建 SQL Server 数据源对象的 OLE DB 驱动程序的实例，与使用者应用程序可以继续通过初始化数据源并创建会话。 OLE DB 会话提供允许数据访问和操作的接口。  
  
 SQL Server 的 OLE DB 驱动程序使其首次连接到的指定实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]作为成功的数据源初始化的一部分。 只要在任一数据源初始化接口，或直到维护引用才会保持连接**IDBInitialize::Uninitialize**调用方法。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [数据源属性 & #40; OLE DB & #41;](../../oledb/ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [数据源信息属性](../../oledb/ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授权属性](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [会话](../../oledb/ole-db-data-source-objects/sessions.md)  
  
-   [会话属性 - 适用于 SQL Server 的 OLE DB 驱动程序](../../oledb/ole-db-data-source-objects/session-properties-oledb-driver-for-sql-server.md)  
  
-   [持久的数据源对象](../../oledb/ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
