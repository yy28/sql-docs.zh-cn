---
title: 释放语句句柄 ODBC |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305612"
---
# <a name="freeing-a-statement-handle-odbc"></a>释放语句句柄 ODBC
如前所述，重用语句比删除语句和分配新语句更有效。 在语句上执行新的 SQL 语句之前，应用程序应确保当前语句设置是合适的。 这些设置包括语句属性、参数绑定和结果集绑定。 通常，旧 SQL 语句的参数和结果集需要取消绑定（使用SQL_RESET_PARAMS和SQL_UNBIND选项调用**SQLFreeStmt），** 并恢复新的 SQL 语句。  
  
 当应用程序完成使用 语句后，它将调用**SQLFreeHandle**来释放该语句。 释放语句后，在调用 ODBC 函数时使用语句的句柄是应用程序编程错误;这样做有未定义，但可能是致命的后果。  
  
 调用**SQLFreeHandle**时，驱动程序将释放用于存储有关语句的信息的结构。  
  
 **SQLDISCONNECT**会自动释放连接上的所有语句。
