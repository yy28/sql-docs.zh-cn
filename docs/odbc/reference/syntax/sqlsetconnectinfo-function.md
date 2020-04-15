---
title: SQLSetConnectInfo 功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b575e0d09f87ad21e1190b8081b6604349a98263
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301848"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 函数
**一致性**  
 版本介绍： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetConnectInfo**用于将数据源、用户 ID 和密码设置为应用程序的[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)调用的连接信息令牌中。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLSetConnectInfo(  
                SQLHDBC_INFO_TOKEN   TokenHandle,  
                WCHAR *              ServerName,  
                SQLSMALLINT          NameLength1,  
                WCHAR *              UserName,  
                SQLSMALLINT          NameLength2,  
                WCHAR *              Authentication,  
                SQLSMALLINT          NameLength3 );  
```  
  
## <a name="arguments"></a>参数  
 *令牌句柄*  
 [输入]令牌句柄。  
  
 *ServerName*  
 [输入]数据源名称。 数据可能位于与程序相同的计算机上，或者位于网络上的另一台计算机上。 有关应用程序如何选择数据源的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [输入]长度 = 以字符表示*服务器名称*。  
  
 *用户*  
 [输入]用户标识符。  
  
 *名称长度2*  
 [输入]长度 =*字符中的用户名*。  
  
 *身份验证*  
 [输入]身份验证字符串（通常是密码）。  
  
 *名称长度3*  
 [输入]长度 =*字符身份验证*。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)一样，用于输入验证错误，只不过驱动程序管理器将使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄类型**和*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>备注  
 每当驱动程序返回SQL_ERROR或SQL_INVALID_HANDLE时，驱动程序管理器都会将错误返回到应用程序（在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中）。  
  
 每当驱动程序返回SQL_SUCCESS_WITH_INFO时，驱动程序管理器将从*hDbcInfoToken*获取诊断信息，并在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO应用程序。  
  
 应用程序不应直接调用此功能。 支持驱动程序感知连接池的 ODBC 驱动程序必须实现此功能。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
