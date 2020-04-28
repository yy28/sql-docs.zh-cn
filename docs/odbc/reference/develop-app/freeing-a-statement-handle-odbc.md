---
title: 释放语句句柄 ODBC |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement handles [ODBC]
- handles [ODBC], statement
- freeing statement handles [ODBC]
ms.assetid: ee18e2f1-2690-4cc1-9e5c-e20244e5d480
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01e4cb46edf1b1a0f1c6dfaa0273c1dd5b392686
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305612"
---
# <a name="freeing-a-statement-handle-odbc"></a>释放语句句柄 ODBC
如前所述，重复使用语句而不是删除和分配新语句更为有效。 在对语句执行新的 SQL 语句之前，应用程序应确保当前语句设置适用。 这些设置包括语句属性、参数绑定和结果集绑定。 通常，旧 SQL 语句的参数和结果集需要未绑定（通过使用 SQL_RESET_PARAMS 和 SQL_UNBIND 选项调用**SQLFreeStmt** ），并为新的 sql 语句重新绑定。  
  
 当应用程序使用完该语句后，它将调用**SQLFreeHandle**来释放该语句。 释放语句后，它是一个应用程序编程错误，用于在对 ODBC 函数的调用中使用语句的句柄;这样做没有定义，但可能会产生严重后果。  
  
 调用**SQLFreeHandle**时，驱动程序将释放用于存储有关语句的信息的结构。  
  
 **SQLDisconnect**自动释放连接上的所有语句。
