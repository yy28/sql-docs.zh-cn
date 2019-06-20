---
title: 声明应用程序&#39;的 ODBC 版本 s |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c5bb124af74d1fa009a61237edb54a9c8baec74
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63267685"
---
# <a name="declaring-the-application39s-odbc-version"></a>声明应用程序&#39;s ODBC 版本
应用程序分配连接之前，它必须设置 SQL_ATTR_ODBC_VERSION 环境属性。 此属性规定应用程序，如下所示 ODBC 2。*x*或 ODBC 3。*x*规范时使用以下各项：  
  
-   **SQLSTATEs**。 许多 SQLSTATE 值是在 ODBC 2 不同。*x*和 ODBC 3。*x*。  
  
-   **日期、 时间和时间戳类型标识符**。 下表显示日期、 时间和 ODBC 2 中的时间戳数据类型标识符。*x*和 ODBC 3。*x*。  
  
    |ODBC 2.*x*|ODBC 3.*x*|  
    |----------------|----------------|  
    |**SQL 类型标识符**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 类型标识符**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_  **SQLTables 中的参数**。 在 ODBC 2。*x*中的通配符字符 （"%"和"_"） *CatalogName*参数按原义处理。 在 ODBC 3。*x*，它们被视为通配符字符。 因此，应用程序的 ODBC 2。*x*规范不能用作这些通配符字符，并且未转义它们时将其用作文本。 遵循 ODBC 3 应用程序。*x*规范可以将这些密钥用作通配符字符或转义它们并将它们用作原义字符。 有关详细信息，请参阅[中目录函数的自变量](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 ODBC 3 *.x*驱动程序管理器和 ODBC 3 *.x*驱动程序检查应用程序写入到的 ODBC 规范的版本，并相应地做出响应。 例如，如果应用程序遵循 ODBC 2。*x*规范并调用**SQLExecute**之前调用**SQLPrepare**，ODBC 3 *.x*驱动程序管理器返回 SQLSTATE S1010 （函数序列错误）。 如果应用程序遵循 ODBC 3 *.x*规范，驱动程序管理器返回 SQLSTATE HY010 （函数序列错误）。 有关详细信息，请参阅[向后兼容性和标准符合性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  请按照 ODBC 3 的应用程序。*x*规范必须使用条件代码来避免使用 ODBC 3 到新的功能。*x*时使用的 ODBC 2。*x*驱动程序。 ODBC 2。*x*驱动程序不支持 ODBC 3 到新的功能。*x*只是因为应用程序声明，它遵循 ODBC 3。*x*规范。 此外，ODBC 3。*x*驱动程序未执行停止支持 ODBC 3 到新的功能。*x*只是因为应用程序声明，它遵循 ODBC 2。*x*规范。
