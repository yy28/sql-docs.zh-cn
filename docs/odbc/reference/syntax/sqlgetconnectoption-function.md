---
title: SQLGetConnectOption 函数 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectOption
helpviewer_keywords:
- SQLGetConnectOption function [ODBC]
ms.assetid: 59cde899-7957-4b5e-8677-f34d3b859bfd
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4a2c04b150f642ff456e6dc814fb7f8a2eca9c1a
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函数
**一致性**  
 版本引入了： ODBC 1.0 标准合规性： 不推荐使用  
  
 **摘要**  
 ODBC 3 中*.x*，ODBC 2*.x*函数**SQLGetConnectOption**已被取代**SQLGetConnectAttr**。 有关详细信息，请参阅[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]  
>  有关什么驱动程序管理器时，将映射此函数可对 ODBC 2*.x*应用程序使用 ODBC 3*.x*驱动程序，请参阅[映射弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)为了向后兼容的附录 g： 驱动程序准则中。  
  
> [!NOTE]  
>  不支持的特性 ODBC 3.8 中引入的 SQL_ASYNC_DBC_FUNCTION_ENABLE **SQLGetConnectOption**。 使用连接句柄上的异步操作的应用程序必须使用**SQLGetConnectAttr**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
