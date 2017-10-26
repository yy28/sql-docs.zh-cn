---
title: "SQLSetStmtOption （桌面数据库驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8d1f51805413056a06c6cee769920e1ad878abe5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption （桌面数据库驱动程序）
|*fOption*|注释|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支持异步处理。 SQL_ASYNC_ENABLE fOption 将返回 SQLSTATE S1C00 （驱动程序不可用）。|  
|SQL_KEYSET_SIZE|唯一有效的键集大小为 0，因为混合和不支持动态游标。 如果此值设置为其他任何数字，它将更改为 0，则调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01s02 的警告 （选项值已更改）。|  
|SQL_MAX_ROWS|唯一有效的行集大小为 0，因为桌面数据库驱动程序不支持限制返回的行数。 如果此值设置为其他任何数字，它将更改为 0，则调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01s02 的警告 （选项值已更改）。|  
|SQL_QUERY_TIMEOUT|不提供支持。|  
|SQL_ROW_NUMBER|不提供支持。|  
|SQL_SIMULATE_CURSOR|不提供支持。|

