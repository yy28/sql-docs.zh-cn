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
manager: craigg
ms.openlocfilehash: e2f731589dcbc10d24ff42d895db60f9f8c054de
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794183"
---
# <a name="returning-sqlnodata"></a>返回 SQL_NO_DATA
当 ODBC *2.x*应用程序 workingwith ODBC *3.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**，并搜索的 update 或 delete 语句已执行但未影响任何行在数据源，ODBC *3.x*驱动程序应返回 SQL_SUCCESS。 当 ODBC *3.x*应用程序使用 ODBC *3.x*驱动程序调用**SQLExecDirect**， **SQLExecute**，或**SQLParamData**具有相同的结果，ODBC *3.x*驱动程序应返回 sql_no_data 为止。  
  
 如果搜索的 update 或 delete 语句在一批语句不会影响任何行在数据源**SQLMoreResults**返回 SQL_SUCCESS。 它不能返回 SQL_NO_DATA，因为这可能意味着没有更多的结果，不是有是从搜索更新/删除受影响任何行的结果。
