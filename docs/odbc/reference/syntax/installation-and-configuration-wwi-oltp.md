---
title: SQLSetDriverConnectInfo Function | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c344315764eac32e2e63663f07b7f797571a0e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63233431"
---
# <a name="sqlsetdriverconnectinfo-function"></a>SQLSetDriverConnectInfo 函数
**符合性**  
 版本引入了：ODBC 3.81 标准符合性：ODBC  
  
 **摘要**  
 **SQLSetDriverConnectInfo**用于为应用程序的连接信息令牌设置连接字符串**SQLDriverConnect**调用。  
  
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
 [输入]完整的连接字符串 (请参阅中的"注释"中的语法[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))，部分连接字符串或为空字符串。  
  
 *StringLength1*  
 [输入]长度 **InConnectionString*，如果该字符串为 Unicode 或字节数，如果字符串为 ANSI 或 DBCS 字符中。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与相同[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)只不过驱动程序管理器将使用与任何输入的验证错误时，相关**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的和一个**处理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>备注  
 每当驱动程序将返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序管理器将错误返回到应用程序 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每当一个驱动程序返回 SQL_SUCCESS_WITH_INFO，驱动程序管理器将获取的诊断信息*hDbcInfoToken*，并返回 SQL_SUCCESS_WITH_INFO 到中的应用程序[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)并[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
