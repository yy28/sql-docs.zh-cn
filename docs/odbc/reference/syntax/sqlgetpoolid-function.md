---
title: SQLGetPoolID 函数 |Microsoft 文档
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
- SQLGetPoolID function [ODBC]
ms.assetid: 95a8666a-ad68-4d89-bf65-f2cc797f8820
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 09e2b9b8176c333b893c5cf7ce9157516b2b368d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32917442"
---
# <a name="sqlgetpoolid-function"></a>SQLGetPoolID 函数
**一致性**  
 版本引入了： ODBC 3.81 标准合规性： ODBC  
  
 **摘要**  
 **SQLGetPoolID**检索池 id。  
  
## <a name="syntax"></a>语法  
  
```  
SQLRETURN  SQLGetPoolID (  
                SQLHDBC_INFO_TOKEN    hDbcInfoToken,  
                POOLID *              pPoolID );  
```  
  
## <a name="arguments"></a>参数  
 *hDbcInfoToken*  
 [输入]包含所有连接信息的令牌句柄。  
  
 *pPoolID*  
 [输出]池 ID，用于标识一组可以互换使用的连接 （有可能会需要其他重置）。  
  
## <a name="returns"></a>返回  
 SQL_SUCCESS、 SQL_SUCCESS_WITH_INFO、 SQL_ERROR 或 SQL_INVALID_HANDLE。  
  
## <a name="diagnostics"></a>诊断  
 当**SQLGetPoolID**返回 SQL_ERROR 或 SQL_SUCCESS_WITH_INFO，驱动程序管理器将使用**HandleType**的 SQL_HANDLE_DBC_INFO_TOKEN 和**处理**的*hDbcInfoToken*。  
  
## <a name="remarks"></a>注释  
 **SQLGetPoolID**用于获取给定的一组连接信息的池 ID (从**SQLSetConnectAttrForDbcInfo**， **SQLSetDriverConnectInfo**，和**SQLSetConnectInfo**)。 此 ID 用于标识一组可以互换使用的连接池 （有可能会需要其他重置）。 池 ID 将用于标识该组的连接的连接池。  
  
 每当驱动程序返回 SQL_ERROR 或 SQL_INVALID_HANDLE，驱动程序管理器会将错误返回到应用程序 (在[SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)或[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md))。  
  
 每当驱动程序返回 SQL_SUCCESS_WITH_INFO，驱动程序管理器将获取诊断信息从*hDbcInfoToken*，并返回到中的应用程序的 SQL_SUCCESS_WITH_INFO [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)和[SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)。  
  
 应用程序不应直接调用此函数。 支持识别驱动程序的连接池的 ODBC 驱动程序必须实现此函数。  
  
 包括 sqlspi.h ODBC 驱动程序的开发。  
  
## <a name="see-also"></a>另请参阅  
 [开发 ODBC 驱动程序](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [识别驱动程序的连接池](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [在 ODBC 驱动程序中开发连接池感知](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)
