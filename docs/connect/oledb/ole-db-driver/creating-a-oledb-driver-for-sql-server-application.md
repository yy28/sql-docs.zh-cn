---
title: 创建适用于 SQL Server 的 OLE DB 驱动程序应用程序 | Microsoft Docs
description: 创建适用于 SQL Server 的 OLE DB 驱动程序应用程序
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 12434c194796244a80c3db79a0e2220607f0d0f4
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43020786"
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>创建适用于 SQL Server 的 OLE DB 驱动程序应用程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  创建 SQL Server 应用程序的 OLE DB 驱动程序涉及以下步骤：  
  
1.  建立与数据源的连接。  
  
2.  执行命令。  
  
3.  结果处理。  
  
> [!NOTE]  
>  请尽可能使用 Windows 身份验证。 如果 Windows 身份验证不可用，请在运行时提示用户输入其凭据。 不要将凭据存储在一个文件中。 如果必须保存凭据，应当用 [Win32 cryptoAPI](http://go.microsoft.com/fwlink/?LinkId=9504) 对它们加密。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [建立与数据源的连接](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [执行命令](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [处理结果](../../oledb/ole-db-driver/processing-results.md)  
  
-   [关于 OLE DB 属性](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [将 OUTPUT 子句与适用于 SQL Server 的 OLE DB 驱动程序中的 OLE DB 结合使用](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>另请参阅  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  
