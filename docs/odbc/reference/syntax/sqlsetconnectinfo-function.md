---
title: "SQLSetConnectInfo 函数 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLSetConnectInfo function [ODBC]
ms.assetid: 0782a1c3-c5d1-499b-a8ba-134162db9990
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f3c5d316a459be5b38a74f9927fee0eee4b85c66
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetconnectinfo-function"></a>SQLSetConnectInfo 函数
**一致性**  
 版本引入了： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetConnectInfo**用于设置数据源、 用户 ID 和密码到应用程序的连接信息令牌[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)调用。  
  
## <a name="syntax"></a>语法  
  
```  
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
 [输入]数据源名称。 数据可能位于与该程序，在同一计算机上，也可以在网络上的某个位置的另一台计算机上。 有关如何应用程序选择数据源的信息，请参阅[选择数据源或驱动程序](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)。  
  
 *NameLength1*  
 [输入]长度 **ServerName*以字符为单位。  
  
 *UserName*  
 [输入]用户标识符。  
  
 *NameLength2*  
 [输入]长度 **用户名*以字符为单位。  
  
 *身份验证*  
 [输入]身份验证字符串 （通常为密码）。  
  
 *NameLength3*  
 [输入]长度 **身份验证*以字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与相同[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)的输入验证错误，只不过驱动程序管理器将使用**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**处理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>Remarks  
 每当驱动程序返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序管理器会将错误返回到应用程序 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每当驱动程序返回 SQL_SUCCESS_WITH_INFO，驱动程序管理器将获取诊断信息从*hDbcInfoToken*，并返回到中的应用程序的 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h ODBC 驱动程序的开发。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
