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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d618a7f845a87394c2fc3c7978a7aef5716e21f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301478"
---
# <a name="sqlsetcursorname-desktop-database-drivers"></a>SQLSetCursorName（桌面数据库驱动程序）
由于驱动程序不支持定位更新或删除，其中当前的*cursorname*语法为，因此支持**SQLSetCursorName** ，但不能用于定位更新。 仅当启用了游标库并且应用程序使用**SQLExtendedFetch**时，才能使用此方法。
