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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f362d725f8b734ab9ecdbdc79c268af08a495b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63313140"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData（桌面数据库驱动程序）
此函数可以从任何列检索数据，无论有绑定的列后它并在其中检索列的顺序无关。  
  
> [!NOTE]  
>  \*在 pcbValue **SQLGetData**可能数两倍字符作为实际可用时返回绑定到 ANSI 数据长度超过 510 个字符，Jet 4.0 数据库上。 小于或等于的 510 字符值将返回实际 cbValue。
