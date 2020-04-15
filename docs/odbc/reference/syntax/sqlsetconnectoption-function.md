---
title: SQLSet连接选项功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 263b15cb75fb5c0c7c1d7aa630a8da171b9765a7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301592"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 已弃用  
  
 **摘要**  
 在 ODBC 3 *.x*中，ODBC 2.0 函数**SQLSetConnectOption**已被**SQLSetConnectAttr**替换。 有关详细信息，请参阅 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]
>  有关驱动程序管理器将此功能映射到 ODBC 2 *.x*应用程序使用 ODBC 3 *.x*驱动程序时的详细信息，请参阅[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)"。  
  
## <a name="remarks"></a>备注  
 如果应用程序将在 64 位操作系统上运行，请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)。  
  
> [!NOTE]  
>  **SQLSetConnectOption**不支持在 ODBC 3.8 中引入的属性SQL_ASYNC_DBC_FUNCTION_ENABLE。 在连接句柄上使用异步操作的应用程序必须使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
