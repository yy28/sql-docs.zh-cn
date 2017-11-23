---
title: "声明应用程序 &#39; s ODBC 版本 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- declaring ODBC version [ODBC]
- data sources [ODBC], declaring ODBC version
- ODBC drivers [ODBC], declaring ODBC version
- connecting to driver [ODBC], declaring ODBC version
- connecting to data source [ODBC], declaring ODBC version
- version declaration [ODBC]
ms.assetid: 083a1ef5-580a-4979-9cf3-50f4549a080a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a58aebc6517268c054a4d2ac92066eb0d0469d2c
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="declaring-the-application39s-odbc-version"></a>声明应用程序 &#39; s ODBC 版本
应用程序分配连接之前，必须设置 SQL_ATTR_ODBC_VERSION 环境属性。 此属性，指出应用程序，如下所示 ODBC 2。*x*或 ODBC 3。*x*规范时使用以下各项：  
  
-   **SQLSTATEs**。 许多 SQLSTATE 值现在 ODBC 2 不同。*x*和 ODBC 3。*x*。  
  
-   **日期、 时间和时间戳类型标识符**。 下表显示日期、 时间和 ODBC 2 中的时间戳数据类型标识符。*x*和 ODBC 3。*x*。  
  
    |ODBC 2。*x*|ODBC 3。*x*|  
    |----------------|----------------|  
    |**SQL 类型标识符**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 类型标识符**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   *CatalogName***中 SQLTables 参数**。 在 ODBC 2。*x*中的通配符字符 （"%"和"_"） *CatalogName*参数按原义处理。 在 ODBC 3。*x*，它们被视为通配符。 因此，应用程序遵循 ODBC 2。*x*规范不能用作这些通配符字符，且未转义它们时将它们用作文本。 遵循 ODBC 3 应用程序。*x*规范可以将这些操作用作通配符字符或转义它们并将它们用作文本。 有关详细信息，请参阅[目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 ODBC 3*.x*驱动程序管理器和 ODBC 3*.x*驱动程序检查应用程序写入到 ODBC 规范的版本，并相应地做出响应。 例如，如果应用程序遵循 ODBC 2。*x*规范和调用**SQLExecute**之前调用**SQLPrepare**，ODBC 3*.x*驱动程序管理器返回 SQLSTATE S1010 （函数序列错误）。 如果应用程序遵循 ODBC 3*.x*规范，驱动程序管理器返回的 SQLSTATE HY010 （函数序列错误）。 有关详细信息，请参阅[向后兼容性和标准合规性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  按照 ODBC 3 的应用程序。*x*规范必须使用条件代码以避免使用 ODBC 3 到新的功能。*x*使用 ODBC 2 时。*x*驱动程序。 ODBC 2。*x*驱动程序不支持 ODBC 3 到新的功能。*x*只是因为应用程序声明，它遵循 ODBC 3。*x*规范。 此外，ODBC 3。*x*驱动程序未执行停止支持 ODBC 3 到新的功能。*x*只是因为应用程序声明，它遵循 ODBC 2。*x*规范。
