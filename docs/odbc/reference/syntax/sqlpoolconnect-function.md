---
title: SQLPoolConnect 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPoolConnect function [ODBC]
ms.assetid: 41322737-890d-4a81-aed2-06cc3d546962
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0c390dacb5072c5d516e95b4fe6b789bfffbbd2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68005799"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 函数
**符合性**  
 版本引入了：ODBC 3.8 标准符合性：ODBC  
  
 **摘要**  
 **SQLPoolConnect**用于创建新的连接，如果没有连接池中可重复使用。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLPoolConnect(  
                SQLHDBC              hDbc,  
                SQLHDBC_INFO_TOKEN   hDbcInfoToken,  
                WCHAR *              wszOutConnectString,  
                SQLSMALLINT          cchConnectStringBuffer,  
                SQLSMALLINT *        cchConnectStringLen );  
```  
  
## <a name="arguments"></a>参数  
 *hDbc*  
 [输入]连接句柄。  
  
 *hDbcInfoToken*  
 [输入]新的应用程序连接请求令牌的句柄。  
  
 *wszOutConnectString*  
 [输出]已完成的连接字符串的缓冲区的指针。 在成功连接到目标数据源，此缓冲区包含已完成的连接字符串。 应用程序应为此缓冲区分配至少 1,024 个字符。  
  
 如果*wszOutConnectString*为 NULL， *cchConnectStringLen*仍将返回的字符 （不包括字符数据的 null 终止字符） 总数可用于在中返回指向缓冲区*wszOutConnectString*。  
  
 *cchConnectStringBuffer*  
 [输入]长度 **wszOutConnectString*缓冲区，以字符为单位。  
  
 *cchConnectStringLen*  
 [输出]指向用于返回的字符 （不包括 null 终止字符） 总数的缓冲区可用于在中返回\* *wszOutConnectString*。 可用于返回的字符数是否大于或等于*cchConnectStringBuffer*，则已完成中的连接字符串\* *wszOutConnectString*截断为*cchConnectStringBuffer*减去 null 终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO，SQL_ERROR，或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 类似于[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)只不过驱动程序管理器将使用的任何输入验证错误时，对于**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的和一个**处理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>备注  
 驱动程序管理器可保证 HENV 处理的父*hDbc*并*hDbcInfoToken*相同。  
  
 与不同[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)，没有任何*DriverCompletion*参数，以提示用户输入连接信息。 一个提示对话框不允许在池的方案。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 每当驱动程序将返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序管理器将错误返回到应用程序 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每当一个驱动程序返回 SQL_SUCCESS_WITH_INFO，驱动程序管理器将获取的诊断信息*hDbcInfoToken*，并返回 SQL_SUCCESS_WITH_INFO 到中的应用程序[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)并[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 当应用程序使用[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)， *wszOutConnectString*将空缓冲区 （最后三个参数将所有设置为 NULL，0，NULL）。 否则，则驱动程序必须返回的输出连接字符串，将返回到应用程序的[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)调用。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
