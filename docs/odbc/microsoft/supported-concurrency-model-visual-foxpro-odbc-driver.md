---
title: 支持并发模型（可视化福克斯Pro ODBC驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], concurrency
- concurrency models [ODBC]
- FoxPro ODBC driver [ODBC], concurrency
ms.assetid: c39ed963-3af1-4888-8631-6083692ddcd7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 253a6dd86f6dc974d53dd151636bb8b8132e4d02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307713"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支持的并发模型（Visual FoxPro ODBC 驱动程序）
可视化福克斯Pro ODBC驱动程序支持*只读并发*。 您的应用程序可以使用SQL_CONCURRENCY选项 SQL_CONCUR_READ_ONLY调用[SQLSetStmtOption。](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md)  
  
 有关详细信息，请参阅[ODBC 程序员的参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>只读并发  
 无法更新游标。  
  
## <a name="row-versioning"></a>行版本控制 (row versioning)  
 本质上是时间戳支持，其中行版本在更新时进行比较。
