---
title: 数据源对象 (OLE DB) |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-ole-db-data-source-objects
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], data source objects
- SQL Server Native Client, data source objects
- SQLNCLI, data source objects
- SQL Server Native Client OLE DB provider, data source objects
- OLE DB data source objects [SQL Server Native Client]
- data source objects [OLE DB]
- CLSID
ms.assetid: c1d4ed20-ad3b-4e33-a26b-38d7517237b7
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 9d8caf5dde7e281a3a67af8ce844a246902ab111
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="data-source-objects-ole-db"></a>数据源对象 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端使用术语数据源的 OLE DB 接口用于建立的链接到数据存储，如集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 创建提供程序的数据源对象的实例是第一项任务的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端使用者。  
  
 每个 OLE DB 访问接口都为自身声明一个类标识符 (CLSID)。 CLSID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序是 C/c + + GUID CLSID_SQLNCLI10 (SQLNCLI_CLSID 将解析为正确的符号 progid 引用 sqlncli.h 文件中)。 对于 CLSID，使用者使用 OLE **CoCreateInstance**函数制造数据源对象的实例。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端是一个进程内服务器。 实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序对象创建 CLSCTX_INPROC_SERVER 宏用于指示可执行上下文。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序数据源对象显示允许的使用者连接到现有的 OLE DB 初始化接口[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
 可通过执行每个连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序会自动设置这些选项：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 此示例使用类标识符宏来创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序数据源对象，并获取对引用其**IDBInitialize**接口。  
  
```  
IDBInitialize*   pIDBInitialize;  
HRESULT          hr;  
  
hr = CoCreateInstance(CLSID_SQLNCLI10, NULL, CLSCTX_INPROC_SERVER,  
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
  
 成功创建的实例与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序数据源对象，使用者应用程序可以继续通过初始化数据源并创建会话。 OLE DB 会话提供允许数据访问和操作的接口。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序使其首次连接到的指定实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为成功的数据源初始化的一部分。 只要在任一数据源初始化接口，或直到维护引用才会保持连接**IDBInitialize::Uninitialize**调用方法。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [数据源属性 & #40; OLE DB & #41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [数据源信息属性](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授权属性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [会话](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [会话属性 - SQL Server Native Client OLE DB 提供程序](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [持久的数据源对象](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
