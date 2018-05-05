---
title: SQLSetScrollOptions （桌面数据库驱动程序） |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5838e890168473cd70d957eb1da6d4be45f546dc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions （桌面数据库驱动程序）
支持对 SQL_CONCUR_READ_ONLY 的正向和静态游标。  
  
 支持仅键集驱动游标*fConcurrency* SQL_CONCUR_LOCK 自变量。  
  
 *FConcurrency* SQL_CONCUR_ROWVER 参数，不支持。  
  
 不支持动态游标和混合的游标。
