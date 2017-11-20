---
title: "释放语句句柄 ODBC |Microsoft 文档"
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
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b33d262c846d9ef8a41bf9440802664ac7d4b75f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="freeing-a-statement-handle-odbc"></a>释放语句句柄 ODBC
如前所述，它会重用比删除它们并分配新的语句更加高效。 之前在一个语句上执行新的 SQL 语句，应用程序应确保当前的语句设置适合。 这些设置包括语句属性、参数绑定和结果集绑定。 通常情况下，参数和旧的 SQL 语句的结果集需要是未绑定 (通过调用**SQLFreeStmt**使用 SQL_RESET_PARAMS 和 SQL_UNBIND 选项) 和新的 SQL 语句的重新绑定。  
  
 当使用语句完成后应用程序时，它将调用**SQLFreeHandle**以释放该语句。 释放该语句之后, 它是对应用程序编程错误对 ODBC 函数; 的调用中使用的语句的句柄因此，这样做具有未定义，但可能严重后果。  
  
 当**SQLFreeHandle**调用时，结构用于存储有关语句的信息的驱动程序版本。  
  
 **SQLDisconnect**自动释放连接上的所有语句。

