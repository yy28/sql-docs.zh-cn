---
title: 数据源对象 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1d0ba930c37d5e2c83093a9aeb6aad835439a8b4
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410256"
---
# <a name="data-source-objects-ole-db"></a>数据源对象 (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 接口用于建立指向数据存储区，如集使用数据源一词[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 创建提供程序的数据源对象的实例是第一个任务的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端使用者。  
  
 每个 OLE DB 访问接口都为自身声明一个类标识符 (CLSID)。 CLSID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口是 C/c + + GUID CLSID_SQLNCLI10 (符号 SQLNCLI_CLSID 将解析为正确 progid 您引用的 sqlncli.h 文件中)。 通过 CLSID，使用者使用 OLE **CoCreateInstance**函数生成的数据源对象的实例。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 是进程内服务器。 实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用 CLSCTX_INPROC_SERVER 宏以指示可执行上下文创建 Native Client OLE DB 提供程序对象。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口数据源对象公开允许使用者连接到现有的 OLE DB 初始化接口[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
 每个连接都通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序将自动设置这些选项：  
  
-   SET ANSI_WARNINGS ON  
  
-   SET ANSI_NULLS ON  
  
-   SET ANSI_PADDING ON  
  
-   SET ANSI_NULL_DFLT_ON ON  
  
-   SET QUOTED_IDENTIFIER ON  
  
-   SET CONCAT_OF_NULL_YIELDS_NULL ON  
  
 此示例中使用类标识符宏来创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序数据源对象，并获取对引用其**IDBInitialize**接口。  
  
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
  
 成功创建的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 访问接口数据源对象，使用者应用程序可以继续通过初始化数据源并创建会话。 OLE DB 会话提供允许数据访问和操作的接口。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序的指定实例的首次连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为成功的数据源初始化的一部分。 只要引用保持对任何数据源初始化接口，或直到保持连接**IDBInitialize::Uninitialize**调用方法。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [数据源属性&#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)  
  
-   [数据源信息属性](../../relational-databases/native-client-ole-db-data-source-objects/data-source-information-properties.md)  
  
-   [初始化和授权属性](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md)  
  
-   [会话](../../relational-databases/native-client-ole-db-data-source-objects/sessions.md)  
  
-   [会话属性 - SQL Server Native Client OLE DB 提供程序](../../relational-databases/native-client-ole-db-data-source-objects/session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [持久化数据源对象](../../relational-databases/native-client-ole-db-data-source-objects/persisted-data-source-objects.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
