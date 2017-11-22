---
title: "SQL Server Native Client ODBC 数据源 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-communication
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, about data sources
- ODBC data sources, names
- data sources [SQL Server Native Client]
- names [ODBC]
- ODBC applications, data sources
- SQL Server Native Client ODBC driver, data sources
- ODBC data sources
ms.assetid: a6a50fd0-d439-43fd-b76f-16ec02f478c5
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 55d639d7c9d3874723439920d3b5d8b13ae5960c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sql-server-native-client-odbc-data-sources"></a>SQL Server Native Client ODBC 数据源
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源名称 (DSN) 标识 ODBC 数据源，此数据源包含 ODBC 应用程序连接到特定服务器上的某个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库所需要的所有信息。 您可以通过两种方法定义 ODBC 数据源名称：  
  
-   在客户端计算机上，在控制面板中打开管理工具和双击**数据源 (ODBC)**。 此时将打开 ODBC 数据源管理器，您可以用它来创建 DSN。  
  
-   ODBC 应用程序，在调用[SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md)。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源包含：  
  
-   数据源的名称。  
  
-   连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特定实例所需的任何信息。  
  
-   要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的特定实例上使用的默认数据库（可选）。  
  
-   相关的设置，如要使用的 ANSI 选项、是否记录性能统计信息等等（可选）。  
  
 不要求将 ODBC 应用程序连接到数据源。 然而，应用程序必须向 ODBC 连接函数提供适当的连接信息，否则驱动程序将在 DSN 中查找相同的连接信息。  
  
## <a name="see-also"></a>另请参阅  
 [通信使用 SQL Server &#40; ODBC &#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
