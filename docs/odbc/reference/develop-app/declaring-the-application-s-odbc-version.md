---
description: 声明应用程序&#39;s ODBC 版本
title: 声明应用程序&#39;s ODBC 版本 |Microsoft Docs
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
ms.openlocfilehash: 0ff41a7a8b56133b0a44947980805c5b46238bad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424711"
---
# <a name="declaring-the-application39s-odbc-version"></a>声明应用程序&#39;s ODBC 版本
在应用程序分配连接之前，必须设置 SQL_ATTR_ODBC_VERSION 环境属性。 此属性指示应用程序在使用以下项目时遵循 ODBC *2.x 或 odbc* *2.x 规范：*  
  
-   **SQLSTATEs**。 许多 SQLSTATE 值*在 odbc* *2.x 和 odbc* 2.x 中是不同的。  
  
-   **日期、时间和时间戳类型标识符**。 下表显示了 ODBC 2.x 和 ODBC 2.x 中的日期、*时间和时间*戳数据的类型*标识符。*  
  
    |ODBC *2.x*|ODBC *2.x*|  
    |----------------|----------------|  
    |**SQL 类型标识符**||  
    |SQL_DATE|SQL_TYPE_DATE|  
    |SQL_TIME|SQL_TYPE_TIME|  
    |SQL_TIMESTAMP|SQL_TYPE_TIMESTAMP|  
    |**C 类型标识符**||  
    |SQL_C_DATE|SQL_C_TYPE_DATE|  
    |SQL_C_TIME|SQL_C_TYPE_TIME|  
    |SQL_C_TIMESTAMP|SQL_C_TYPE_TIMESTAMP|  
  
-   _CatalogName_**SQLTables 中的 CatalogName 参数**。   在 ODBC *2.x 中，* *CatalogName* 参数中的通配符 ( "%" 和 "_" ) 按原义处理。 在 ODBC *3.x 中，* 它们被视为通配符。 因此， *遵循 ODBC 2.x* 规范的应用程序不能将它们用作通配符，并且在将它们用作文本时不会将其转义。 遵循 *ODBC 2.x* 规范的应用程序可以将它们用作通配符或对它们进行转义，并将它们用作文本。 有关详细信息，请参阅 [目录函数中的参数](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)。  
  
 *Odbc 2.X 驱动程序管理*器*和 odbc 2.x 驱动程序将*检查应用程序所写入的 ODBC 规范的版本，并相应地做出响应。 例如，如果应用程序遵循 ODBC *2.x 规范并*在调用**SQLPrepare**之前调用**SQLExecute** ，*则 ODBC 1.X*驱动程序管理器将返回 SQLSTATE S1010 (函数序列错误) 。 如果应用程序 *遵循 ODBC 1.x* 规范，驱动程序管理器将返回 SQLSTATE HY010 (函数序列错误) 。 有关详细信息，请参阅 [向后兼容性和标准符合性](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)。  
  
> [!IMPORTANT]  
>  遵循*odbc 2.x 规范的*应用程序必须使用条件代码，以避免在*使用 odbc 2.x 驱动*程序*时，* 将新功能用于 odbc 2.x。 ODBC *2.x 驱动程序不支持 odbc 2.x*的新功能，*只是*因为应用程序声明它遵循 odbc *2.x 规范。* 此外，ODBC *2.x 驱动程序*不会停止支持 odbc 2.x 的新功能，*只是*因为应用程序声明它遵循 odbc *2.x 规范。*
