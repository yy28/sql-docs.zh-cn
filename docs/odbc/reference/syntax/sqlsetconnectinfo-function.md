---
title: SQLSetConnectInfo Function | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 448b0f5e34a6b7421c23a1267dd9cd68bd93ca6f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537179"
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 函数
**符合性**  
 版本引入了：ODBC 3.81 标准符合性：ODBC  
  
 **摘要**  
 **SQLSetConnectInfo**用于为应用程序的连接信息令牌设置数据源、 用户 ID 和密码[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)调用。  
  
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
 *TokenHandle*  
 [输入]标记句柄。  
  
 *ServerName*  
 [输入]数据源名称。 数据可能不位于该程序，在同一台计算机上，也可以在网络上的某个位置的另一台计算机上。 有关应用程序如何选择数据源的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [输入]长度 **ServerName*以字符为单位。  
  
 *UserName*  
 [输入]用户标识符。  
  
 *NameLength2*  
 [输入]长度 **用户名*以字符为单位。  
  
 *身份验证*  
 [输入]身份验证的字符串 （通常是密码）。  
  
 *NameLength3*  
 [输入]长度 **身份验证*以字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与相同[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)的输入验证错误，只不过驱动程序管理器将使用**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的和一个**处理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>备注  
 每当驱动程序将返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序管理器将错误返回到应用程序 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每当一个驱动程序返回 SQL_SUCCESS_WITH_INFO，驱动程序管理器将获取的诊断信息*hDbcInfoToken*，并返回 SQL_SUCCESS_WITH_INFO 到中的应用程序[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)并[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
