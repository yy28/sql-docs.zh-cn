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
manager: craigg
ms.openlocfilehash: 62d22d1bf5fc3d01bf62afd2da6b3ebbc2bb0289
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62742263"
---
# <a name="sqlsetconnectoption-function"></a>SQLSetConnectOption 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：不推荐使用  
  
 **摘要**  
 在 ODBC 3 *.x*，ODBC 2.0 函数**SQLSetConnectOption**已由**SQLSetConnectAttr**。 有关详细信息，请参阅 [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)。  
  
> [!NOTE]
>  有关哪些驱动程序管理器时，将映射此函数可对 ODBC 2 详细信息 *.x*应用程序使用 ODBC 3 *.x*驱动程序，请参阅[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)".  
  
## <a name="remarks"></a>备注  
 请参阅[ODBC 64-Bit 信息](../../../odbc/reference/odbc-64-bit-information.md)，如果你的应用程序将在 64 位操作系统上运行。  
  
> [!NOTE]  
>  不支持属性符合 ODBC 3.8 中引入的 SQL_ASYNC_DBC_FUNCTION_ENABLE **SQLSetConnectOption**。 使用连接句柄上的异步操作的应用程序必须使用**SQLSetConnectAttr**。  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
