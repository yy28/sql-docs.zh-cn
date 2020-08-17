---
description: SQLGetData（桌面数据库驱动程序）
title: SQLGetData (桌面数据库驱动程序) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cfce744c3f4a2e0e4d9fcb054a8226538537bdcf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340224"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData（桌面数据库驱动程序）
无论列是否有绑定列，此函数都可以从任何列中检索数据，而不考虑检索列的顺序。  
  
> [!NOTE]  
>  \*在 Jet 4.0 数据库上绑定到超过510个字符的 ANSI 数据时， **SQLGetData** 中的 pcbValue 可能会返回实际可用字符数的两倍。 大于或等于510的字符值将返回实际的 cbValue。
