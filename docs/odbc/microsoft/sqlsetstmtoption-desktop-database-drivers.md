---
description: SQLSetStmtOption（桌面数据库驱动程序）
title: SQLSetStmtOption (桌面数据库驱动程序) |Microsoft Docs
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
ms.openlocfilehash: 0696ee98dd88f1c23120ef1d96c6e8d93751f76e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449149"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption（桌面数据库驱动程序）

|*fOption*|注释|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支持异步处理。 SQL_ASYNC_ENABLE fOption 将返回 SQLSTATE S1C00 (驱动程序无法) 。|  
|SQL_KEYSET_SIZE|唯一有效的键集大小为0，因为不支持混合和动态游标。 如果此值设置为其他任何数字，则将其更改为0，并且调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 (选项值) 更改。|  
|SQL_MAX_ROWS|唯一有效的行集大小为0，因为桌面数据库驱动程序不支持限制返回的行数。 如果此值设置为其他任何数字，则将其更改为0，并且调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 (选项值) 更改。|  
|SQL_QUERY_TIMEOUT|不支持。|  
|SQL_ROW_NUMBER|不支持。|  
|SQL_SIMULATE_CURSOR|不支持。|
