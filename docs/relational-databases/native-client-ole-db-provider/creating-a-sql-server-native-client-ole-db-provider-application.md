---
title: "创建 SQL Server Native Client OLE DB 提供程序应用程序 |Microsoft 文档"
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-provider
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc7e0c3b21625501b0538d03f5fbf507643e78d3
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>创建 SQL Server Native Client OLE DB 访问接口应用程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  创建[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序应用程序涉及以下步骤：  
  
1.  建立与数据源的连接。  
  
2.  执行命令。  
  
3.  结果处理。  
  
> [!NOTE]  
>  请尽可能使用 Windows 身份验证。 如果 Windows 身份验证不可用，请在运行时提示用户输入其凭据。 不要将凭据存储在一个文件中。 如果你必须保存凭据，应将它们与加密[Win32 cryptoAPI](http://go.microsoft.com/fwlink/?LinkId=9504)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [建立与数据源的连接](../../relational-databases/native-client-ole-db-provider/establishing-a-connection-to-a-data-source.md)  
  
-   [执行命令](../../relational-databases/native-client-ole-db-provider/executing-a-command.md)  
  
-   [处理结果](../../relational-databases/native-client-ole-db-provider/processing-results.md)  
  
-   [关于 OLE DB 属性](../../relational-databases/native-client-ole-db-provider/about-ole-db-properties.md)  
  
-   [在 SQL Server Native Client 中使用 OUTPUT 子句 (OLE DB)](../../relational-databases/native-client-ole-db-provider/using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server Native Client (OLE DB)](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
