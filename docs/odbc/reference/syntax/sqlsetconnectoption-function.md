---
title: SQLSetConnectOption 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetConnectOption
helpviewer_keywords:
- SQLSetConnectOption function [ODBC]
ms.assetid: 8cd2c2a2-25c8-4aff-951c-b593bbfc90ad
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b429e499cccaad553236b4ebee78374c69c7c4dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093009"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函数
**度**  
 引入的版本： ODBC 1.0 标准符合性：已弃用  
  
 **总结**  
 在 ODBC 3.x*中，odbc*2.0 函数**SQLSetConnectOption**已被**SQLSetConnectAttr**取代。 有关详细信息，请参阅 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]
>  有关 ODBC 2.x 应用程序使用 ODBC 2.x*驱动程序时*，驱动程序管理器将此函数映射到的内容的详细** 信息，请参阅[映射弃用的函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)"。  
  
## <a name="remarks"></a>备注  
 如果你的应用程序将在64位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
> [!NOTE]  
>  **SQLSetConnectOption**不支持 ODBC 3.8 中引入的属性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 使用连接句柄上的异步操作的应用程序必须使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
