---
title: 声明应用程序&#39;其 ODBC 版本 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba346ed7f7a261446110c5513026d20a86fd3a19
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285227"
---
# <a name="declaring-the-application39s-odbc-version"></a>声明应用程序&#39;其 ODBC 版本
在应用程序分配连接之前，它必须设置SQL_ATTR_ODBC_VERSION环境属性。 此属性指出，当使用以下项时，应用程序遵循 ODBC *2.x*或 ODBC *3.x*规范：  
  
-   **SQLSTATEs**. 许多 SQLSTATE 值在 ODBC *2.x*和 ODBC *3.x*中是不同的。  
  
-   **日期、时间和时间戳类型标识符**。 下表显示了 ODBC *2.x*和 ODBC *3.x*中日期、时间和时间戳数据的类型标识符。  
  
    |ODBC *2.x*|ODBC *3.x*|  
    |----------------|----------------|  
    |**SQL 类型标识符**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 类型标识符**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _SQLTables 中的目录名称_  **参数**。 在 ODBC *2.x*中，*目录名称*参数中的通配符（"%"和"+"）从字面上处理。 在 ODBC *3.x*中，它们被视为通配符。 因此，遵循 ODBC *2.x*规范的应用程序不能将这些字符用作通配符，并且在将它们用作文本时不会转义它们。 遵循 ODBC *3.x*规范的应用程序可以将这些字符用作通配符或转义它们，并将其用作文本。 有关详细信息，请参阅[目录函数 中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 ODBC *3.x*驱动程序管理器和 ODBC *3.x*驱动程序检查编写应用程序的 ODBC 规范的版本并做出相应响应。 例如，如果应用程序遵循 ODBC *2.x*规范，并在调用**SQLPrepare**之前调用**SQLExecute，** 则 ODBC *3.x*驱动程序管理器返回 SQLSTATE S1010（函数序列错误）。 如果应用程序遵循 ODBC *3.x*规范，驱动程序管理器将返回 SQLSTATE HY010（函数序列错误）。 有关详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  遵循 ODBC *3.x*规范的应用程序必须使用条件代码，以避免在使用 ODBC *2.x*驱动程序时使用 ODBC *3.x*新增功能。 ODBC *2.x*驱动程序不支持 ODBC *3.x*新增的功能，只是因为应用程序声明它遵循 ODBC *3.x*规范。 此外，ODBC *3.x*驱动程序不会仅仅因为应用程序声明遵循 ODBC *2.x*规范而停止支持 ODBC *3.x*新增功能。
