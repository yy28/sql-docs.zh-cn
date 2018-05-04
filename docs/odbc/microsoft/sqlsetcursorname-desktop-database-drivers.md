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
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be029ce99030aab9ae72e40648e211af1a7d7dee
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName （桌面数据库驱动程序）
因为该驱动程序不支持定位的更新或删除由 WHERE CURRENT OF *cursorname*语法， **SQLSetCursorName**支持，但不能用于定位的更新。 它仅可在时才启用光标库和应用程序使用**SQLExtendedFetch**。
