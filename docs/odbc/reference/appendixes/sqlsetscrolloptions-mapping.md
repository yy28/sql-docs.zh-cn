---
title: SQLSetScrollOptions 映射 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetScrollOptions
ms.assetid: a0fa4510-8891-4a61-a867-b2555bc35f05
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4339f395ae4c554a7ad8ca2e554769d8b27cdd4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 映射
在应用程序调用**SQLSetScrollOptions**到 ODBC 3 *.x*驱动程序和驱动程序不支持**SQLSetScrollOptions**，对的调用  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 将导致，如下所示：  
  
-   对的调用  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     与*信息类型*参数设置为下表中，根据的值中的值之一*KeysetSize*中的参数**SQLSetScrollOptions**。  
  
    |*KeysetSize 自变量*|*信息类型参数*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |值比大*RowsetSize*自变量|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果值*KeysetSize*自变量未列出在前面的表中，调用**SQLSetScrollOptions**返回 SQLSTATE S1107 （行值超出了范围） 且当前没有的以下步骤执行。  
  
     驱动程序管理器然后验证是否在中设置相应的位 **InfoValuePtr*调用返回的值**SQLGetInfo**，根据值*并发*中的参数**SQLSetScrollOptions**。  
  
    |*并发*自变量|*信息类型*设置|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果*并发*参数不是上表中，对的调用中的值之一**SQLSetScrollOptions**返回 SQLSTATE S1108 （超出范围的并发选项） 且当前没有的以下步骤执行。 如果未设置 （作为前面的表中指示） 的相应位 **InfoValuePtr*到对应的值之一*并发*自变量，将会调用**SQLSetScrollOptions**返回 SQLSTATE S1C00 （驱动程序不支持的信息） 和不执行任何以下步骤。  
  
-   对的调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     与 *\*ValuePtr*设置为下表中，根据的值中的值之一*KeysetSize*中的参数**SQLSetScrollOptions**。  
  
    |*KeysetSize*自变量|*\*ValuePtr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |值比大*RowsetSize*自变量|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   对的调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     与 *\*ValuePtr*设置为*并发*中的参数**SQLSetScrollOptions**。  
  
-   如果*KeysetSize*对的调用中的自变量**SQLSetScrollOptions**为正，对的调用  
  
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
    >  当驱动程序管理器映射**SQLSetScrollOptions**为应用程序使用 ODBC 3 *.x*驱动程序不支持**SQLSetScrollOptions**，驱动程序管理器将设置 SQL_ROWSET_SIZE 语句选项，不 SQL_ATTR_ROW_ARRAY_SIZE 语句特性，为*RowsetSize*中的参数**SQLSetScrollOption**。 因此， **SQLSetScrollOptions**按调用提取多行时，应用程序不使用**SQLFetch**或**SQLFetchScroll**。 仅当通过调用提取多个行时，才可以使用它**SQLExtendedFetch**。
