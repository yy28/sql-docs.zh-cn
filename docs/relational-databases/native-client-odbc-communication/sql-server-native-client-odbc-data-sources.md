---
title: SQL Server Native Client ODBC 数据源 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
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
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 4553908f106528ce87dfdea268e0257959551da4
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35702508"
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
  
## <a name="see-also"></a>请参阅  
 [与 SQL Server 通信&#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
