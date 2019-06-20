---
title: 定长书签 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], bookmarks
- bookmarks [ODBC]
- compatibility [ODBC], bookmarks
- fixed-length bookmarks [ODBC]
ms.assetid: cbd8185e-fb03-408f-b80b-1a2e164534fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e40947dc4dbad0830444870ea7e2d0c663490b25
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188967"
---
# <a name="fixed-length-bookmarks"></a>定长书签
如果 ODBC 3 *.x*驱动程序都应适用于 ODBC 2。*x*使用定长书签，驱动程序必须支持以下应用程序：  
  
-   SQL_UB_ON 作为 SQL_USE_BOOKMARKS 语句选项的值。 (在 ODBC 3 中已弃用 SQL_UB_ON *.x*。)  
  
-   SQL_GET_BOOKMARK 语句选项。
