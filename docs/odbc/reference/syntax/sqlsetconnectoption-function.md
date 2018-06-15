---
title: SQLSetConnectOption 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 965a563620dc95720602b03091dd38507cfa1e08
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916902"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： 不推荐使用  
  
 **摘要**  
 ODBC 3 中 *.x*，ODBC 2.0 函数**SQLSetConnectOption**已被取代**SQLSetConnectAttr**。 有关详细信息，请参阅 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]  
>  有关什么驱动程序管理器时，将映射此函数可对 ODBC 2 *.x*应用程序使用 ODBC 3 *.x*驱动程序，请参阅[映射弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>注释  
 请参阅[ODBC 64 位信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
> [!NOTE]  
>  不支持的特性 ODBC 3.8 中引入的 SQL_ASYNC_DBC_FUNCTION_ENABLE **SQLSetConnectOption**。 使用连接句柄上的异步操作的应用程序必须使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
