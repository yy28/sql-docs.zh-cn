---
title: 分配环境句柄 |微软文档
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e8020f8e29de1c8c765f288336e806d4a9ce15b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307749"
---
# <a name="allocating-an-environment-handle"></a>分配环境句柄
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  在应用程序可以调用任何 ODBC 函数之前，它必须初始化 ODBC 环境并分配环境句柄。 这是全局上下文句柄，并且是 ODBC 中其他句柄的占位符。 为此，通过将*处理类型*参数设置为SQL_HANDLE_ENV和*输入句柄*设置为SQL_NULL_HANDLE调用**SQLAllocHandle。**  
  
 分配环境句柄之后，应用程序必须设置环境属性以指示它将使用哪一个版本的 ODBC 函数调用。 使用 ODBC 3。*x*函数，调用[SQLSetEnvAttr，](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)*将属性*参数设置为SQL_ATTR_ODBC_VERSION，ValuePtr 设置为SQL_OV_ODBC3。 *ValuePtr*  
  
## <a name="see-also"></a>另请参阅  
 [与 SQL 服务器通信 &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
