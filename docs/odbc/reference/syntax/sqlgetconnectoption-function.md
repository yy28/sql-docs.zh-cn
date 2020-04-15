---
title: SQLGetConnectOption 功能 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94a29637365862990ea067f663023fae04a7af3e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285567"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函数
**一致性**  
 版本介绍： ODBC 1.0 标准合规性： 已弃用  
  
 **摘要**  
 在 ODBC *3.x*中，ODBC *2.x*函数**SQLGetConnectOption**已被**SQLGetConnectAttr**替换。 有关详细信息，请参阅[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]
>  有关驱动程序管理器将此功能映射到 ODBC *2.x*应用程序使用 ODBC *3.x*驱动程序时的详细信息，请参阅附录 G：向后兼容性驱动程序指南中的[映射已弃用函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)。  
> 
> [!NOTE]
>  **SQLGetConnectOption**不支持在 ODBC 3.8 中引入的属性SQL_ASYNC_DBC_FUNCTION_ENABLE。 在连接句柄上使用异步操作的应用程序必须使用**SQLGetConnectAttr**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
