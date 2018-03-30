---
title: 为 SQL Server 应用程序创建 OLE DB 驱动程序 |Microsoft 文档
description: 创建 SQL Server 应用程序用于 OLE DB 驱动程序
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e54bdee09a64cd1393a41109207d42a598cb31fa
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>为 SQL Server 应用程序创建 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  创建 SQL Server 应用程序用于 OLE DB 驱动程序涉及以下步骤：  
  
1.  建立与数据源的连接。  
  
2.  执行命令。  
  
3.  结果处理。  
  
> [!NOTE]  
>  请尽可能使用 Windows 身份验证。 如果 Windows 身份验证不可用，请在运行时提示用户输入其凭据。 不要将凭据存储在一个文件中。 如果你必须保存凭据，应将它们与加密[Win32 cryptoAPI](http://go.microsoft.com/fwlink/?LinkId=9504)。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [建立与数据源的连接](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [执行命令](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [处理结果](../../oledb/ole-db-driver/processing-results.md)  
  
-   [有关 OLE DB 属性](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [使用 OLE DB 驱动程序中的 OLE DB 中使用 OUTPUT 子句，用于 SQL Server](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [用于 SQL Server 的 OLE DB 驱动程序&#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
  
  
