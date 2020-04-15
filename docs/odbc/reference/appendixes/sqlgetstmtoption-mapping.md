---
title: SQLGetStmtOption 映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetStmtOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLGetStmtOption
ms.assetid: fa599517-3f3e-4dad-a65a-b8596ae3f330
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68819269d41407f2ce9dee172c889f7d7f286793
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300597"
---
# <a name="sqlgetstmtoption-mapping"></a>SQLGetStmtOption 映射
当应用程序将**SQLGetStmtOption**调用不支持它的 ODBC *3.x*驱动程序时，调用  
  
```  
SQLGetStmtOption(hstmt, fOption, pvParam)  
```  
  
 结果如下：  
  
-   如果*fOption*指示返回字符串的 ODBC 定义的语句选项，驱动程序管理器将调用  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
-   如果*fOption*指示一个 ODBC 定义的语句选项，该选项返回 32 位整数值，则驱动程序管理器将调用  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, 0, NULL)  
    ```  
  
-   如果*fOption*指示驱动程序定义的语句选项，则驱动程序管理器将调用  
  
    ```  
    SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, NULL)  
    ```  
  
 在前面三种情况下，*语句句柄*参数设置为*hstmt*中的值，*属性*参数设置为*fOption*中的值 *，ValuePtr*参数设置为与*pvParam*相同的值。  
  
 对于 ODBC 定义的字符串连接选项，驱动程序管理器在调用**SQLGetConnectAttr**时将*缓冲区长度*参数设置为预定义的最大长度（SQL_MAX_OPTION_STRING_LENGTH）;对于非字符串连接选项，*缓冲区长度*设置为 0。  
  
 SQL_GET_BOOKMARK语句选项已在 ODBC *3.x*中弃用。 对于使用SQL_GET_BOOKMARK的 ODBC *3.x*驱动程序*2.x*，它必须支持SQL_GET_BOOKMARK。 对于 ODBC *3.x*驱动程序，必须支持*2.x*将SQL_USE_BOOKMARKS设置为SQL_UB_ON，并且应公开固定长度的书签。 如果 ODBC *3.x*驱动程序仅支持可变长度书签，不支持固定长度书签，则必须返回 SQLSTATE HYC00（未实现可选功能）（如果 ODBC *2.x*应用程序尝试将SQL_USE_BOOKMARKS设置为SQL_UB_ON。  
  
 对于 ODBC *3.x*驱动程序，驱动程序管理器不再检查*选项*是否介于SQL_STMT_OPT_MIN和SQL_STMT_OPT_MAX之间，还是大于SQL_CONNECT_OPT_DRVR_START。 驱动程序必须检查此情况。
