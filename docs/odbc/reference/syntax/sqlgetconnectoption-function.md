---
title: SQLGetConnectOption 函数 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 947a7ea107e334eb393248f7d368fe958e6229c0
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792581"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函数
**符合性**  
 版本引入了：ODBC 1.0 标准符合性：不推荐使用  
  
 **摘要**  
 在 ODBC *3.x*，ODBC *2.x*函数**SQLGetConnectOption**已由**SQLGetConnectAttr**。 有关详细信息，请参阅[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]
>  详细了解驱动程序管理器映射的内容到此函数时 ODBC *2.x*应用程序使用 ODBC *3.x*驱动程序，请参阅[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)附录 g:为了向后兼容的驱动程序指南。  
> 
> [!NOTE]
>  不支持属性符合 ODBC 3.8 中引入的 SQL_ASYNC_DBC_FUNCTION_ENABLE **SQLGetConnectOption**。 使用连接句柄上的异步操作的应用程序必须使用**SQLGetConnectAttr**。  
  
## <a name="see-also"></a>请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
