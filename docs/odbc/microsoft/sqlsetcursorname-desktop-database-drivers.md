---
title: SQLSetCursorName （桌面数据库驱动程序） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e433e6aee341085965f361992fc8ea9ac8744353
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305633"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName（桌面数据库驱动程序）
因为该驱动程序不支持定位的更新或删除 WHERE CURRENT OF *cursorname*语法**SQLSetCursorName**支持，但不能用于定位更新。 它只能使用游标库启用并使用该应用程序时**SQLExtendedFetch**。
