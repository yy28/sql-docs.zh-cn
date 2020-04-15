---
title: SQLSetConnectOption 映射 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 757b50c7e18133e02b4cf6addaa327b2053f5439
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287467"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 映射
当一个ODBC 2。*x*应用程序通过 ODBC 3 *.x*驱动程序调用**SQLSetConnectOption，** 调用  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 结果如下：  
  
-   如果*fOption*指示需要字符串的 ODBC 定义的连接属性，驱动程序管理器将调用  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示返回 32 位整数值的 ODBC 定义的连接属性，则驱动程序管理器将调用  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驱动程序定义的连接属性，则驱动程序管理器将调用  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 在前面三种情况下 *，ConnectHandle*参数设置为*hdbc*中的值，*属性*参数设置为*fOption*中的值 *，ValuePtr*参数设置为与*vParam*相同的值。  
  
 由于驱动程序管理器不知道驱动程序定义的连接属性是否需要字符串还是 32 位整数值，因此必须为**SQLSetConnectAttr**的*BufferLength*参数传递有效值。 如果驱动程序为驱动程序定义的连接属性定义了特殊语义，并且需要使用**SQLSetConnectOption**调用 ，则必须支持**SQLSetConnectOption**。  
  
 如果 ODBC 2.*x*应用程序调用**SQLSetConnectOption**在 ODBC 3 *.x*驱动程序中设置特定于驱动程序的语句选项，该选项在 ODBC 2 中定义。*驱动程序*的 x 版本，应为 ODBC 3 *.x*驱动程序中的选项定义新的清单常量。 如果在调用**SQLSetConnectOption**时使用旧的清单常量，驱动程序管理器将调用**SQLSetConnectAttr，****字符串长度**参数设置为 0。  
  
 对于 ODBC 3 *.x*驱动程序，驱动程序管理器不再检查*fOption*是否位于SQL_CONN_OPT_MIN和SQL_CONN_OPT_MAX之间，还是大于SQL_CONNECT_OPT_DRVR_START。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>在连接级别上设置语句选项  
 在 ODBC 2 中。*x*，应用程序可以调用**SQLSetConnectOption**来设置语句选项。 完成此操作后，驱动程序将语句选项作为以后为该连接分配的任何语句的默认值。 驱动程序是否为与指定连接关联的任何现有语句设置语句选项，由驱动程序定义。  
  
 此能力已在 ODBC 3 *.x*中被弃用。 ODBC 3 *.x*驱动程序只需要支持设置 ODBC 2。*x*语句属性在连接级别，如果他们想与 ODBC 2 一起工作。*x*执行此操作的应用程序。 ODBC 3 *.x*应用程序绝不应在连接级别设置语句属性。 ODBC 3 *.x*语句属性无法在连接级别设置，但SQL_ATTR_METADATA_ID和SQL_ATTR_ASYNC_ENABLE属性除外，这些属性既是连接属性，也是语句属性，可以在连接级别或语句级别进行设置。
