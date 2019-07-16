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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 638cf9fb3c7af73130cf1413559b9baee2a354c1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069782"
---
# <a name="freeing-a-statement-handle-odbc"></a>释放语句句柄 ODBC
前面曾提到，是重复使用比删除它们并分配新的语句更有效。 在执行前的新的 SQL 语句的语句，应用程序应确保当前的语句设置正确。 这些设置包括语句属性、参数绑定和结果集绑定。 通常情况下，参数和旧的 SQL 语句的结果集需要是未绑定 (通过调用**SQLFreeStmt** SQL_RESET_PARAMS 和 SQL_UNBIND 选项) 和新的 SQL 语句的重新绑定。  
  
 当应用程序使用完该语句时，它将调用**SQLFreeHandle**释放语句。 释放该语句后, 是编程错误应用程序使用 ODBC 函数; 调用中的语句的句柄这样做存在未定义，但可能严重后果。  
  
 当**SQLFreeHandle**调用时，该结构用于存储有关语句的信息的驱动程序版本。  
  
 **SQLDisconnect**自动释放连接上的所有语句。
