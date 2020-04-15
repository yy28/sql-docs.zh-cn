---
title: SQLSetDriverConnectInfo 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10336475e39598161126c13771ad822de0d5f7d8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298793"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函数
**一致性**  
 版本介绍： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetDriverConnectInfo**用于将连接字符串设置为应用程序的**SQLDriverConnect**调用的连接信息令牌。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>参数  
 *令牌句柄*  
 [输入]令牌句柄。  
  
 *连接字符串*  
 [输入]完整的连接字符串（请参阅[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中的"注释"中的语法）、部分连接字符串或空字符串。  
  
 *字符串长度1*  
 [输入]如果字符串为 Unicode，则长度 =*连接字符串*，或字符串为 ANSI 或 DBCS 的字节。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与与任何输入验证错误相关的[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)相同，只不过驱动程序管理器将使用 SQL_HANDLE_DBC_INFO_TOKEN 的**句柄类型**和*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>备注  
 每当驱动程序返回SQL_ERROR或SQL_INVALID_HANDLE时，驱动程序管理器都会将错误返回到应用程序（在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中）。  
  
 每当驱动程序返回SQL_SUCCESS_WITH_INFO时，驱动程序管理器将从*hDbcInfoToken*获取诊断信息，并在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO应用程序。  
  
 应用程序不应直接调用此功能。 支持驱动程序感知连接池的 ODBC 驱动程序必须实现此功能。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
