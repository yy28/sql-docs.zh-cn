---
title: 分配的环境句柄 |Microsoft 文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-communication
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7c12f1bfb5c14cb9bb7f65eed3870be3713d461d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="allocating-an-environment-handle"></a>分配环境句柄
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  在应用程序可以调用任何 ODBC 函数之前，它必须初始化 ODBC 环境并分配环境句柄。 这是全局上下文句柄，并且是 ODBC 中其他句柄的占位符。 执行此操作通过调用**SQLAllocHandle**与*HandleType*参数设置为 SQL_HANDLE_ENV 和*InputHandle*设置为 SQL_NULL_HANDLE。  
  
 分配环境句柄之后，应用程序必须设置环境属性以指示它将使用哪一个版本的 ODBC 函数调用。 若要使用 ODBC 3。*x*函数调用[SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)与*属性*参数设置为 SQL_ATTR_ODBC_VERSION 和*ValuePtr*设置为 SQL_OV_ODBC3。  
  
## <a name="see-also"></a>另请参阅  
 [与 SQL Server 通信&#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
