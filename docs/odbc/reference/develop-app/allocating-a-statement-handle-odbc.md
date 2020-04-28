---
title: 分配语句句柄 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9a15bc4622b15afa9838327edd90383a812270
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288427"
---
# <a name="allocating-a-statement-handle-odbc"></a>分配语句句柄 ODBC
在应用程序可以执行语句之前，它必须分配语句句柄，如下所示：  
  
1.  应用程序声明类型为 HSTMT 的变量。 然后，它调用**SQLAllocHandle**并传递此变量的地址、要在其中分配语句的连接的句柄和 SQL_HANDLE_STMT 选项。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驱动程序管理器分配一个结构，在该结构中存储有关语句的信息并使用 SQL_HANDLE_STMT 选项调用驱动程序中的**SQLAllocHandle** 。  
  
3.  驱动程序将分配其自己的结构，以便在其中存储有关语句的信息并将驱动程序语句句柄返回到驱动程序管理器。  
  
4.  驱动程序管理器将驱动程序管理器语句句柄返回到应用程序变量中的应用程序。  
  
 语句句柄标识在调用 ODBC 函数时要使用的语句。 有关语句句柄的详细信息，请参阅[语句句柄](../../../odbc/reference/develop-app/statement-handles.md)。
