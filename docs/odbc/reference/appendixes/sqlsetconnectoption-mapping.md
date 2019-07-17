---
title: SQLSetConnectOption 映射 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b512a795c3b9e2d1c6aa1c7c9e92fbc42a8c7862
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125591"
---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 映射
当 ODBC 2。*x*应用程序调用**SQLSetConnectOption**通过 ODBC 3 *.x*驱动程序，将会调用  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 将生成按如下所示：  
  
-   如果*fOption*指示必须为字符串，该驱动程序管理器调用 ODBC 定义的连接属性  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示返回 32 位整数值，驱动程序管理器调用 ODBC 定义的连接属性  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驱动程序定义的连接属性，驱动程序管理器调用  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 在前面的三种情况下， *ConnectionHandle*参数设置为中的值*hdbc*，则*特性*参数设置中的值为*fOption*，并*ValuePtr*参数设置为相同的值*vParam*。  
  
 驱动程序管理器不知道驱动程序定义的连接属性需要字符串或 32 位整数值，因为它必须是有效的值传入*BufferLength*自变量的**SQLSetConnectAttr**. 如果该驱动程序定义了特殊语义的驱动程序定义连接属性，需要使用来调用**SQLSetConnectOption**，则它必须支持**SQLSetConnectOption**。  
  
 如果检测到 ODBC 2。*x*应用程序调用**SQLSetConnectOption**若要将驱动程序特定的语句选项设置在 ODBC 3 *.x* ODBC 2 中定义驱动程序和选项。*x*应为 ODBC 3 中的选项定义版本的驱动程序，新的清单常量 *.x*驱动程序。 如果在调用中使用旧清单常量**SQLSetConnectOption**，驱动程序管理器将调用**SQLSetConnectAttr**与**StringLength**参数设置为 0。  
  
 对于 ODBC 3 *.x*驱动程序，驱动程序管理器不再检查以查看是否*fOption*介于 SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX，或者大于 SQL_CONNECT_OPT_DRVR_START。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>在连接级别上设置语句选项  
 在 ODBC 2。*x*，应用程序可以调用**SQLSetConnectOption**以设置语句选项。 完成后，该驱动程序建立默认情况下的启用语句选项的更高版本分配给该连接的任何语句。 它是驱动程序定义的驱动程序是否设置与指定的连接关联的任何现有语句的语句选项。  
  
 此功能已弃用在 ODBC 3 *.x*。 ODBC 3 *.x*驱动程序仅需支持设置 ODBC 2。*x*在连接级别，如果用户想要使用 ODBC 2 的语句属性。*x*执行此操作的应用程序。 ODBC 3 *.x*应用程序应永远不会在连接级别设置语句属性。 ODBC 3 *.x*不能在连接级别，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，这是连接属性和语句属性，并且可以设置语句属性设置在连接级别或语句级别。
