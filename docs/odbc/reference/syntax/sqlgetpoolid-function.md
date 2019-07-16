---
title: SQLGetPoolID 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7daef4785a77df294a831d69089108cbb1d88489
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68061477"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 函数
**符合性**  
 版本引入了：ODBC 3.81 标准符合性：ODBC  
  
 **摘要**  
 **SQLGetPoolID**检索池 id。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>参数  
 *hDbcInfoToken*  
 [输入]令牌的句柄，包含所有连接信息。  
  
 *pPoolID*  
 [输出]用于标识一组可以互换使用的连接池 ID （可能需要其他重置）。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetPoolID**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，驱动程序管理器将使用**HandleType** SQL_HANDLE_DBC_INFO_TOKEN 的和一个**处理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>备注  
 **SQLGetPoolID**用于获取给定的一组连接信息的池 ID (从**SQLSetConnectAttrForDbcInfo**， **SQLSetDriverConnectInfo**，并**SQLSetConnectInfo**)。 此 ID 用于标识一组可以互换使用的连接池 （可能需要其他重置）。 池 ID 将用于标识该组的连接的连接池。  
  
 每当驱动程序将返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序管理器将错误返回到应用程序 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每当一个驱动程序返回 SQL_SUCCESS_WITH_INFO，驱动程序管理器将获取的诊断信息*hDbcInfoToken*，并返回 SQL_SUCCESS_WITH_INFO 到中的应用程序[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)并[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h 的 ODBC 驱动程序开发。  
  
## <a name="see-also"></a>请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
