---
title: SQLGetPoolID 函数 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32cc973f4dab5bde7bcedade0365d233987dda72
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303314"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 函数
**一致性**  
 版本介绍： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLGetPoolID**检索池 ID。  
  
## <a name="syntax"></a>语法  
  
```cpp
  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>参数  
 *hDbcInfoToken*  
 [输入]包含所有连接信息的令牌句柄。  
  
 *pPoolID*  
 [输出]池 ID，用于标识一组可互换使用的连接（可能需要额外重置）。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、SQL_SUCCESS_WITH_INFO、SQL_ERROR或SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetPoolID**返回SQL_ERROR或SQL_SUCCESS_WITH_INFO时，驱动程序管理器将使用SQL_HANDLE_DBC_INFO_TOKEN的**句柄类型**和*hDbcInfoToken*的**句柄**。  
  
## <a name="remarks"></a>备注  
 **SQLGetPoolID**用于获取给定一组连接信息的池 ID（来自**SQLSetConnectAttrForDbcInfo、SQLSetDriverConnectInfo**和**SQLSetConnectInfo）。** **SQLSetDriverConnectInfo** 此池 ID 用于标识一组可互换使用的连接（可能需要额外重置）。 池 ID 将用于标识该组连接的连接池。  
  
 每当驱动程序返回SQL_ERROR或SQL_INVALID_HANDLE时，驱动程序管理器都会将错误返回到应用程序（在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中）。  
  
 每当驱动程序返回SQL_SUCCESS_WITH_INFO时，驱动程序管理器将从*hDbcInfoToken*获取诊断信息，并在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)中返回SQL_SUCCESS_WITH_INFO应用程序。  
  
 应用程序不应直接调用此功能。 支持驱动程序感知连接池的 ODBC 驱动程序必须实现此功能。  
  
 包括用于 ODBC 驱动程序开发的 sqlspi.h。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [驱动程序感知连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
