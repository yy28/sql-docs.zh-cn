---
title: SQLSetStmtOption （桌面数据库驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299407"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption（桌面数据库驱动程序）

|*fOption*|说明|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支持异步处理。 SQL_ASYNC_ENABLE fOption 将返回 SQLSTATE S1C00 （不支持驱动程序）。|  
|SQL_KEYSET_SIZE|唯一有效的键集大小为0，因为不支持混合和动态游标。 如果此值设置为其他任何数字，则将其更改为0，并且调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （选项值已更改）。|  
|SQL_MAX_ROWS|唯一有效的行集大小为0，因为桌面数据库驱动程序不支持限制返回的行数。 如果此值设置为其他任何数字，则将其更改为0，并且调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （选项值已更改）。|  
|SQL_QUERY_TIMEOUT|不支持。|  
|SQL_ROW_NUMBER|不支持。|  
|SQL_SIMULATE_CURSOR|不支持。|
