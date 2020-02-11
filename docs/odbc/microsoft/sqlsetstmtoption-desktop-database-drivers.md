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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 20043c96771bf888defa2c8fbeb028aaa18f5abc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905344"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption（桌面数据库驱动程序）

|*fOption*|注释|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|不支持异步处理。 SQL_ASYNC_ENABLE fOption 将返回 SQLSTATE S1C00 （不支持驱动程序）。|  
|SQL_KEYSET_SIZE|唯一有效的键集大小为0，因为不支持混合和动态游标。 如果此值设置为其他任何数字，则将其更改为0，并且调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （选项值已更改）。|  
|SQL_MAX_ROWS|唯一有效的行集大小为0，因为桌面数据库驱动程序不支持限制返回的行数。 如果此值设置为其他任何数字，则将其更改为0，并且调用将返回 SQL_SUCCESS_WITH_INFO 和 SQLSTATE 01S02 （选项值已更改）。|  
|SQL_QUERY_TIMEOUT|不支持。|  
|SQL_ROW_NUMBER|不支持。|  
|SQL_SIMULATE_CURSOR|不支持。|
