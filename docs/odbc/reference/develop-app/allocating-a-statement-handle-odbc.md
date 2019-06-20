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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9524f2e6b01d2a5827dcface3159b7c52a728c59
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287872"
---
# <a name="allocating-a-statement-handle-odbc"></a>分配语句句柄 ODBC
应用程序可执行语句之前，必须分配语句句柄，如下所示：  
  
1.  应用程序声明类型 HSTMT 的变量。 然后，它调用**SQLAllocHandle** ，并将传递此变量，用来将语句和 SQL_HANDLE_STMT 选项分配连接句柄的地址。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驱动程序管理器分配要在其中存储有关的语句和调用信息的结构**SQLAllocHandle** SQL_HANDLE_STMT 选项与驱动程序中。  
  
3.  驱动程序分配其自己要在其中存储有关语句的信息的结构，并返回到驱动程序管理器的驱动程序语句句柄。  
  
4.  驱动程序管理器返回到应用程序变量中的应用程序的驱动程序管理器的语句句柄。  
  
 语句句柄标识调用 ODBC 函数时要使用哪个语句。 语句句柄的详细信息，请参阅[语句句柄](../../../odbc/reference/develop-app/statement-handles.md)。
