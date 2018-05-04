---
title: 支持并发模型 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档
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
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 18f555f32ed05914d325ba4664e952d4488f787b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支持的并发模型 （Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序支持*只读并发*。 你的应用程序可以调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CONCUR_READ_ONLY SQL_CONCURRENCY 选项。  
  
 有关详细信息，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>只读的并发  
 无法更新光标。  
  
## <a name="row-versioning"></a>行版本控制 (row versioning)  
 实质上是时间戳的支持，版本在更新时在哪一行的比较。
