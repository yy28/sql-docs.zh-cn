---
title: 数据源对象 (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
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
ms.openlocfilehash: 6b602695720e0d6567e44e4fbe8fd06b6d496a6e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084288"
---
# <a name="data-source-objects-ole-db"></a>数据源对象 (OLE DB)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 接口用于建立指向数据存储区，如集使用数据源一词[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 创建提供程序的数据源对象的实例是第一个任务的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端使用者。  
  
 每个 OLE DB 访问接口都为自身声明一个类标识符 (CLSID)。 CLSID [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 访问接口是 C/c + + GUID CLSID_SQLNCLI10 (符号 SQLNCLI_CLSID 将解析为正确 progid 您引用的 sqlncli.h 文件中)。 通过 CLSID，使用者使用 OLE CoCreateInstance 函数生成数据源对象的实例。  
  
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
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序的指定实例的首次连接[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]作为成功的数据源初始化的一部分。 只要保持对数据源初始化接口的引用，或者在调用 IDBInitialize::Uninitialize 方法前，这一连接会一直保持。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [数据源属性 (OLE DB)](data-source-properties-ole-db.md)  
  
-   [数据源信息属性](data-source-information-properties.md)  
  
-   [初始化和授权属性](initialization-and-authorization-properties.md)  
  
-   [会话](sessions.md)  
  
-   [会话属性](session-properties-sql-server-native-client-ole-db-provider.md)  
  
-   [持久化数据源对象](persisted-data-source-objects.md)  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client (OLE DB)](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
