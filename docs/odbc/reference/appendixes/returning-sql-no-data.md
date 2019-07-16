---
title: 返回 sql_no_data 指示到达 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2613593d9c2e20d5dfa01c0a0b4f9886dbc8e889
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057130"
---
# <a name="returning-sqlnodata"></a>返回 SQL_NO_DATA
当 ODBC *2.x*应用程序 workingwith ODBC *3.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，并搜索的 update 或 delete 语句已执行但未影响任何行在数据源，ODBC *3.x*驱动程序应返回 SQL_SUCCESS。 当 ODBC *3.x*应用程序使用 ODBC *3.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**具有相同的结果，ODBC *3.x*驱动程序应返回 sql_no_data 为止。  
  
 如果搜索的 update 或 delete 语句在一批语句不会影响任何行在数据源**SQLMoreResults**返回 SQL_SUCCESS。 它不能返回 SQL_NO_DATA，因为这可能意味着没有更多的结果，不是有是从搜索更新/删除受影响任何行的结果。
