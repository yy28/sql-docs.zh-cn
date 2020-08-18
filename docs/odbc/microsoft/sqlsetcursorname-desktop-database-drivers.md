---
description: SQLSetCursorName（桌面数据库驱动程序）
title: SQLSetCursorName (桌面数据库驱动程序) |Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14fe15c6cdbdf50e6d28ca7e9a1168f54626e83b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411548"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName（桌面数据库驱动程序）
由于驱动程序不支持定位更新或删除，其中当前的 *cursorname* 语法为，因此支持 **SQLSetCursorName** ，但不能用于定位更新。 仅当启用了游标库并且应用程序使用 **SQLExtendedFetch**时，才能使用此方法。
