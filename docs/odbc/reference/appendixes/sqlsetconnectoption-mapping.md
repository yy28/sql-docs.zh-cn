---
title: "SQLSetConnectOption 映射 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e531888390bbe4f625d308ad983059634e84ba2b
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetconnectoption-mapping"></a>SQLSetConnectOption 映射
当一个 ODBC 2。*x*应用程序调用**SQLSetConnectOption**到 ODBC 3*.x*驱动程序，将会调用  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 将导致，如下所示：  
  
-   如果*fOption*指示必须为字符串，驱动程序管理器调用 ODBC 定义连接属性  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   如果*fOption*指示返回一个 32 位整数值，驱动程序管理器调用 ODBC 定义连接属性  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   如果*fOption*指示驱动程序定义连接特性，则驱动程序管理器调用  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 在前面的三种情况下， *ConnectionHandle*参数设置中的值为*hdbc*、*属性*参数设置中的值为*fOption*，和*ValuePtr*参数设置为相同的值*vParam*。  
  
 驱动程序管理器不知道驱动程序定义的连接属性需要字符串或 32 位整数值，因此可以传递中的有效值*BufferLength*参数**SQLSetConnectAttr**. 如果该驱动程序已定义了特殊语义的驱动程序定义连接属性并需要使用来调用**SQLSetConnectOption**，则它必须支持**SQLSetConnectOption**。  
  
 如果检测到 ODBC 2。*x*应用程序调用**SQLSetConnectOption**在 ODBC 3 中设置特定于驱动程序的语句选项*.x*驱动程序，以及该选项已在 ODBC 2 中定义。*x*应为 ODBC 3 中的选项定义版本的驱动程序，新的清单常量*.x*驱动程序。 如果在调用中使用旧的清单常量**SQLSetConnectOption**，驱动程序管理器将调用**SQLSetConnectAttr**与**StringLength**参数设置为 0。  
  
 ODBC 3*.x*驱动程序，驱动程序管理器不再将检查以查看*fOption* SQL_CONN_OPT_MIN 和 SQL_CONN_OPT_MAX，之间或大于 SQL_CONNECT_OPT_DRVR_START。  
  
## <a name="setting-statement-options-on-the-connection-level"></a>设置连接级别的语句选项  
 在 ODBC 2。*x*，应用程序可以调用**SQLSetConnectOption**设置语句选项。 在驱动程序完成后，建立默认情况下的语句选项对于更高版本为该连接分配任何语句。 它是驱动程序定义的驱动程序是否将设置与指定连接关联的任何现有语句的语句选项。  
  
 此功能已弃用 ODBC 3 中*.x*。 ODBC 3*.x*驱动程序需要仅支持设置 ODBC 2。*x*语句属性在连接级别，如果他们想要使用 ODBC 2。*x*执行此操作的应用程序。 ODBC 3*.x*应用应永远不会将语句属性设置在连接级别。 ODBC 3*.x*语句属性不能在连接级别，除了 SQL_ATTR_METADATA_ID 和 SQL_ATTR_ASYNC_ENABLE 属性，这是连接属性和语句特性，可以设置在连接级别或语句级上设置。

