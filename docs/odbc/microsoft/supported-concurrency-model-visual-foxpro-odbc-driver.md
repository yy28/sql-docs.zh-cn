---
title: "支持并发模型 （Visual FoxPro ODBC 驱动程序） |Microsoft 文档"
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
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9f3348850a76bb831c236fd1c1ee49fb89b97504
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支持的并发模型 （Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序支持*只读并发*。 你的应用程序可以调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CONCUR_READ_ONLY SQL_CONCURRENCY 选项。  
  
 有关详细信息，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>只读的并发  
 无法更新光标。  
  
## <a name="row-versioning"></a>行版本控制 (row versioning)  
 实质上是时间戳的支持，版本在更新时在哪一行的比较。
