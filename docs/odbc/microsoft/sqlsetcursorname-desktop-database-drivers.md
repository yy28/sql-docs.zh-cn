---
title: "SQLSetCursorName （桌面数据库驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLSetCursorName function [ODBC], Desktop Database Drivers
ms.assetid: 9bd7c87b-d99d-4e23-b2db-868d3b461c94
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ee0a3a3d5aa5404a062a11410f0ae2adf072e240
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName （桌面数据库驱动程序）
因为该驱动程序不支持定位的更新或删除由 WHERE CURRENT OF *cursorname*语法， **SQLSetCursorName**支持，但不能用于定位的更新。 它仅可在时才启用光标库和应用程序使用**SQLExtendedFetch**。

