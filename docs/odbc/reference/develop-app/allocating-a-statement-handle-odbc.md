---
title: 分配语句句柄 ODBC |Microsoft 文档
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
- SQL statements [ODBC], statement handles
- statement handles [ODBC]
- allocating statement handles [ODBC]
- handles [ODBC], statement
ms.assetid: 4ce3b446-34ab-46dc-96e5-f40ec95c267e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d0f2bd2da071bb690443df9d5c0bdebb5a5e1e6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908902"
---
# <a name="allocating-a-statement-handle-odbc"></a>分配语句句柄 ODBC
应用程序可以执行语句，它必须先分配然后语句句柄，如下所示：  
  
1.  应用程序声明类型 HSTMT 的变量。 然后，它调用**SQLAllocHandle**并将传递此变量，用于从中分配中的语句，并 SQL_HANDLE_STMT 选项中的连接的句柄的地址。 例如：  
  
    ```  
    SQLHSTMT hstmt1;  
  
    SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);  
    ```  
  
2.  驱动程序管理器分配要在其中存储有关的语句和调用信息的结构**SQLAllocHandle** SQL_HANDLE_STMT 选项与驱动程序中。  
  
3.  驱动程序分配要在其中存储有关语句的信息自己结构，并返回到驱动程序管理器的驱动程序语句句柄。  
  
4.  驱动程序管理器返回到应用程序变量中的应用程序的驱动程序管理器语句句柄。  
  
 语句句柄标识调用 ODBC 函数时要使用的语句。 有关语句句柄的详细信息，请参阅[语句句柄](../../../odbc/reference/develop-app/statement-handles.md)。
