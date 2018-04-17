---
title: SQLSetCursorName （桌面数据库驱动程序） |Microsoft 文档
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
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f68d1503d928ab93b3e7d208141eeb065ae9450e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName （桌面数据库驱动程序）
因为该驱动程序不支持定位的更新或删除由 WHERE CURRENT OF *cursorname*语法， **SQLSetCursorName**支持，但不能用于定位的更新。 它仅可在时才启用光标库和应用程序使用**SQLExtendedFetch**。
