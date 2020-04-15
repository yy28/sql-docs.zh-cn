---
title: SQLSetScroll 选项映射 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77050df283b10abd17ba62a48bd366d6c1b3f601
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300497"
---
# <a name="sqlsetscrolloptions-mapping"></a>SQLSetScrollOptions 映射
当应用程序通过 ODBC *3.x*驱动程序调用**SQLSetScrollOptions，** 并且驱动程序不支持**SQLSetScrollOptions**时，调用  
  
```  
SQLSetScrollOptions(StatementHandle, Concurrency, KeysetSize, RowsetSize)  
```  
  
 结果如下：  
  
-   呼叫  
  
    ```  
    SQLGetInfo(ConnectionHandle, InfoType, InfoValuePtr, BufferLength, StringLengthPtr)  
    ```  
  
     InfoType*InfoType*参数设置为下表中的一个值，具体取决于**SQLSetScrollOptions**中的*KeysetSize*参数的值。  
  
    |*键集大小参数*|*信息类型参数*|  
    |---------------------------|-------------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_STATIC|SQL_STATIC_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
    |SQL_SCROLL_DYNAMIC|SQL_DYNAMIC_CURSOR_ATTRIBUTES2|  
    |大于*RowsetSize*参数的值|SQL_KEYSET_CURSOR_ATTRIBUTES2|  
  
     如果上表中未列出*KeysetSize*参数的值，则对**SQLSetScrollOptions 的**调用将返回 SQLSTATE S1107（行值不在范围范围内），并且不执行以下步骤。  
  
     然后，驱动程序管理器根据**SQLSetScrollOptions**中*并发*参数的值，验证是否在调用**SQLGetInfo**返回的 #*InfoValuePtr*值中设置了适当的位。  
  
    |*并发*参数|*信息类型*设置|  
    |----------------------------|------------------------|  
    |SQL_CONCUR_READ_ONLY|SQL_CA2_READ_ONLY_CONCURRENCY|  
    |SQL_CONCUR_LOCK|SQL_CA2_LOCK_CONCURRENCY|  
    |SQL_CONCUR_ROWVER|SQL_CA2_ROWVER_CONCURRENCY|  
    |SQL_CONCUR_VALUES|SQL_CA2_VALUES_CONCURRENCY|  
  
     如果*并发*参数不是上表中的值之一，则对**SQLSetScrollOption 的**调用将返回 SQLSTATE S1108（在范围外不变选项），并且不执行以下步骤。 如果未在 #*InfoValuePtr*中设置相应的位（如上表所示），则对**SQLSetScrollOptions**的*Concurrency*调用将返回 SQLSTATE S1C00（驱动程序无法执行），并且不执行以下步骤。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CURSOR_TYPE, ValuePtr, 0)  
    ```  
  
     根据**SQLSetScrollOptions**中的*KeysetSize*参数的值*\*，ValuePtr*设置为下表中的一个值。  
  
    |*键集大小*参数|*\*价值Ptr*|  
    |---------------------------|------------------|  
    |SQL_SCROLL_FORWARD_ONLY|SQL_CURSOR_FORWARD_ONLY|  
    |SQL_SCROLL_STATIC|SQL_CURSOR_STATIC|  
    |SQL_SCROLL_KEYSET_DRIVEN|SQL_CURSOR_KEYSET_DRIVEN|  
    |SQL_SCROLL_DYNAMIC|SQL_CURSOR_DYNAMIC|  
    |大于*RowsetSize*参数的值|SQL_CURSOR_KEYSET_DRIVEN|  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_CONCURRENCY, ValuePtr, 0)  
    ```  
  
     将*\*ValuePtr*设置为**SQLSetScrollOptions**中的*并发*参数。  
  
-   如果对**SQLSetScrollOptions**的调用中的*KeysetSize*参数为正参数，则调用  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ATTR_KEYSET_SIZE, ValuePtr, 0)  
    ```  
  
     将*\*ValuePtr*设置为**SQLSetScroll 选项**中的*KeysetSize*参数。  
  
-   呼叫  
  
    ```  
    SQLSetStmtAttr(StatementHandle, SQL_ROWSET_SIZE, ValuePtr, 0)  
    ```  
  
     将*\*ValuePtr*设置为**SQLSetScroll 选项**中的*RowsetSize*参数。  
  
    > [!NOTE]  
    >  当驱动程序管理器映射**SQLSetScrollOption 的应用程序 SQLSetScrollOption**时，使用不支持**SQLSetScrollOption**的 ODBC *3.x*驱动程序时，驱动程序管理器将SQL_ROWSET_SIZE语句选项（而不是SQL_ATTR_ROW_ARRAY_SIZE语句属性）设置为**SQLSetScrollOption**中的*RowsetSize*参数。 因此，当调用**SQLFetch**或**SQLFetchScroll**获取多行时，应用程序无法使用**SQLSetScrollOptions。** 它只能在调用**SQLExtendedFetch**获取多行时使用。
