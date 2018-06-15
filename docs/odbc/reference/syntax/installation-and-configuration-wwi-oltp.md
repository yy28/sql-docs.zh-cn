---
title: SQLSetDriverConnectInfo 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDriverConnectInfo function [ODBC]
ms.assetid: bfd4dfc2-fbca-4ef3-81e5-2706f2389256
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63dee07cc01051f42fa6552a38d99dd7678f7ab8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916734"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函数
**一致性**  
 版本引入了： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLSetDriverConnectInfo**用于设置连接字符串到应用程序的连接信息令牌**SQLDriverConnect**调用。  
  
## <a name="syntax"></a>语法  
  
```  
SQLRETURN SQLSetDriverConnectInfo(  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              InConnectionString,  
                SQLSMALLINT          StringLength1 );  
```  
  
## <a name="arguments"></a>参数  
 *TokenHandle*  
 [输入]标记句柄。  
  
 *InConnectionString*  
 [输入]完整连接字符串 (请参阅中的"注释"中的语法[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))，部分连接字符串或空字符串。  
  
 *StringLength1*  
 [输入]长度 **InConnectionString*，以如果字符串为 Unicode 或字节，如果字符串为 ANSI 或 DBCS 字符为单位。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与相同[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)只不过驱动程序管理器将使用与任何输入的验证错误时，相关**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**处理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>注释  
 每当驱动程序返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序管理器会将错误返回到应用程序 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每当驱动程序返回 SQL_SUCCESS_WITH_INFO，驱动程序管理器将获取诊断信息从*hDbcInfoToken*，并返回到中的应用程序的 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h ODBC 驱动程序的开发。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
