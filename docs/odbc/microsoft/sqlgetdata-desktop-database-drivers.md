---
title: "SQLGetData （桌面数据库驱动程序） |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cdf875d594d84143ec45afca22805e533837c676
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData （桌面数据库驱动程序）
此函数可以从任何列中，检索数据，无论存在绑定的列之后以及在其中检索列的顺序。  
  
> [!NOTE]  
>  \*中的 pcbValue **SQLGetData**可能会返回两倍数量为实际可用的字符时，绑定到 ANSI 数据长度超过 510 个字符在 Jet 4.0 数据库上。 字符值小于或等于的 510 将返回实际 cbValue。
