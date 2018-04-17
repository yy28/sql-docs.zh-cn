---
title: SQLSetStmtOption （桌面数据库驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 765f61337b28e1791d9853bbc26b057375084749
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
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
