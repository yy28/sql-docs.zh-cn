---
title: SQLPool连接功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5045fe47683529f858b01e69f6af696e2821ca4c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306898"
---
# <a name="sqlpoolconnect-function"></a>SQLPoolConnect 函数
**一致性**  
 版本介绍： ODBC 3.8 标准合规性： ODBC  
  
 **摘要**  
 如果池中无法重用任何连接，**则 SQLPoolConnect**用于创建新连接。  
  
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
 *赫德布*  
 [输入]连接句柄。  
  
 *hDbcInfoToken*  
 [输入]新应用程序连接请求的令牌句柄。  
  
 *wszOutConnectString*  
 [输出]指向已完成连接字符串的缓冲区。 成功连接到目标数据源后，此缓冲区包含已完成的连接字符串。 应用程序应为此缓冲区分配至少 1，024 个字符。  
  
 如果*wszOutConnectString*为*NULL，cchConnectStringLen*仍将返回可用在*wszOutConnectString*指向的缓冲区中返回的字符总数（不包括字符数据的空终止字符）。  
  
 *cchConnectString缓冲区*  
 [输入]**wszOutConnectString*缓冲区的长度（以字符表示）。  
  
 *cchConnectStringLen*  
 [输出]指向一个缓冲区的指针，其中返回可在\**wszOutConnectString*中返回的字符总数（不包括空终止字符）。 如果可供返回的字符数大于或等于*cchConnectStringBuffer，*\**则 wszOutConnectString*中已完成的连接字符串将被截断为*cchConnectStringBuffer*减去空终止字符的长度。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 与[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)的任何输入验证错误类似，只不过驱动程序管理器将使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄类型**和*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>备注  
 驱动程序管理器保证 hDbc 和*hDbcInfoToken*的父 HENV 句柄相同。 *hDbc*  
  
 与[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)不同，没有*驱动程序完成*参数来提示用户输入连接信息。 在池化方案中不允许提示对话框。  
  
 应用程序不应直接调用此功能。 支持驱动程序感知连接池的 ODBC 驱动程序必须实现此功能。  
  
 每当驱动程序返回SQL_ERROR或SQL_INVALID_HANDLE时，驱动程序管理器都会将错误返回到应用程序（在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中）。  
  
 每当驱动程序返回SQL_SUCCESS_WITH_INFO时，驱动程序管理器将从*hDbcInfoToken*获取诊断信息，并在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO应用程序。  
  
 当应用程序使用[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)时 *，wszOutConnectString*将是一个 NULL 缓冲区（最后三个参数将全部设置为 NULL、0、NULL）。 否则，驱动程序必须返回输出连接字符串，该字符串将返回到应用程序的[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)调用。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
