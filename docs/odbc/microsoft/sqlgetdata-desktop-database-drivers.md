---
title: SQLGetData （桌面数据库驱动程序） |Microsoft Docs
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
ms.openlocfilehash: 2b102d8435831d45aad3c2049581513e0493de9a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304118"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData（桌面数据库驱动程序）
无论列是否有绑定列，此函数都可以从任何列中检索数据，而不考虑检索列的顺序。  
  
> [!NOTE]  
>  \*在 Jet 4.0 数据库上绑定到超过510个字符的 ANSI 数据时， **SQLGetData**中的 pcbValue 可能会返回实际可用字符数的两倍。 大于或等于510的字符值将返回实际的 cbValue。
