---
title: SQLSetScrollOptions Mapping | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5520554b509b0c25d62e4a191e16ad3524a02652
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297463"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 映射
当应用程序调用**SQLSetScrollOptions**通过 ODBC 3 *.x*驱动程序和驱动程序不支持**SQLSetScrollOptions**，对的调用  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 将生成按如下所示：  
  
-   对的调用  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     与*信息类型*参数设置为下表中，具体取决于值中的值之一*KeysetSize*中的参数**SQLSetScrollOptions**。  
  
    |*KeysetSize 参数*|*信息类型参数*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |值大于*RowsetSize*参数|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果的值*KeysetSize*自变量上的表中，对的调用中未列出**SQLSetScrollOptions**返回 SQLSTATE S1107 （行超出范围的值），没有以下的步骤执行。  
  
     然后，驱动程序管理器验证是否在中设置相应的位 **InfoValuePtr*调用返回的值**SQLGetInfo**的值根据*并发*中的参数**SQLSetScrollOptions**。  
  
    |*并发*参数|*信息类型*设置|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果*并发*参数不是上表中，对的调用中的值之一**SQLSetScrollOptions**返回 SQLSTATE S1108 （超出范围的并发选项），没有以下的步骤执行。 如果未设置 （即在上表中） 的相应位 **InfoValuePtr*对应的值之一*并发*参数，将会调用**SQLSetScrollOptions**返回 SQLSTATE S1C00 （驱动程序不支持） 和不执行任何以下步骤。  
  
-   对的调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     与 *\*ValuePtr*设置为下表中，根据的值中的值之一*KeysetSize*中的参数**SQLSetScrollOptions**。  
  
    |*KeysetSize*参数|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |值大于*RowsetSize*参数|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   对的调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     与 *\*ValuePtr*设置为*并发*中的参数**SQLSetScrollOptions**。  
  
-   如果*KeysetSize*调用中的参数**SQLSetScrollOptions**是正数，对的调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     与 *\*ValuePtr*设置为*KeysetSize*中的参数**SQLSetScrollOptions**。  
  
-   对的调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     与 *\*ValuePtr*设置为*RowsetSize*中的参数**SQLSetScrollOptions**。  
  
    > [!NOTE]  
    >  当驱动程序管理器映射**SQLSetScrollOptions**应用程序使用 ODBC 3 *.x*不支持的驱动程序**SQLSetScrollOptions**，驱动程序管理器将设置 SQL_ROWSET_SIZE 语句选项，不将 SQL_ATTR_ROW_ARRAY_SIZE 语句属性，为*RowsetSize*中的参数**SQLSetScrollOption**。 因此， **SQLSetScrollOptions**由在调用提取多行时，应用程序不能使用**SQLFetch**或**SQLFetchScroll**。 仅当通过调用提取多行时，可以使用它**SQLExtendedFetch**。
