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
ms.openlocfilehash: 7461304a9aa015eac223dc726e669ad5c4ecd4ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68103827"
---
# <a name="sqlgetconnectoption-function"></a>SQLGetConnectOption 函数
**度**  
 引入的版本： ODBC 1.0 标准符合性：已弃用  
  
 **总结**  
 在 ODBC 3.x*中，odbc* *2.x 函数* **SQLGetConnectOption**已被**SQLGetConnectAttr**取代。 有关详细信息，请参阅[SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)。  
  
> [!NOTE]
>  有关 ODBC *2.x 应用程序**使用 odbc 2.x*驱动程序时，驱动程序管理器将此函数映射到的内容的详细信息，请参阅附录 G：驱动程序准则中的[映射弃用的函数](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)以实现向后兼容性。  
> 
> [!NOTE]
>  **SQLGetConnectOption**不支持 ODBC 3.8 中引入的属性 SQL_ASYNC_DBC_FUNCTION_ENABLE。 使用连接句柄上的异步操作的应用程序必须使用**SQLGetConnectAttr**。  
  
## <a name="see-also"></a>另请参阅  
 [ODBC API 参考](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 头文件](../../../odbc/reference/install/odbc-header-files.md)
