---
title: SQLSetScrollOptions （桌面数据库驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e74a3207691aca001dcf334c1ee50d53d4f34d69
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305701"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions（桌面数据库驱动程序）
为 SQL_CONCUR_READ_ONLY 支持正向和静态游标。  
  
 为支持仅由键集驱动游标*fConcurrency* SQL_CONCUR_LOCK 参数。  
  
 *FConcurrency* SQL_CONCUR_ROWVER 参数不受支持。  
  
 不支持动态游标和混合的游标。
