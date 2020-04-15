---
title: SQLSetStmtOption（桌面数据库驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69b386aee3f95fd047f72510dce7658130ac7aa5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299407"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption（桌面数据库驱动程序）

|*fOption*|注释|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支持异步处理。 SQL_ASYNC_ENABLE fOption 将返回 SQLSTATE S1C00（驱动程序无法使用）。|  
|SQL_KEYSET_SIZE|唯一有效的键集大小为 0，因为不支持混合游标和动态游标。 如果此值设置为任何其他号码，它将更改为 0，并且调用将返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02（选项值已更改）。|  
|SQL_MAX_ROWS|唯一有效的行集大小为 0，因为桌面数据库驱动程序不支持限制返回的行数。 如果此值设置为任何其他号码，它将更改为 0，并且调用将返回SQL_SUCCESS_WITH_INFO和 SQLSTATE 01S02（选项值已更改）。|  
|SQL_QUERY_TIMEOUT|不支持。|  
|SQL_ROW_NUMBER|不支持。|  
|SQL_SIMULATE_CURSOR|不支持。|
