---
title: 固定长度书签 |Microsoft 文档
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
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c94d79500047fe1f918689426846a3faa98bb2d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="fixed-length-bookmarks"></a>固定长度书签
如果 ODBC 3 *.x*驱动程序都应适用于 ODBC 2。*x*使用固定长度书签，驱动程序必须支持以下应用程序：  
  
-   SQL_UB_ON 作为 SQL_USE_BOOKMARKS 语句选项的值。 (在 ODBC 3 中已弃用 SQL_UB_ON *.x*。)  
  
-   SQL_GET_BOOKMARK 语句选项。
