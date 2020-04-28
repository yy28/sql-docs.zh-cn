---
title: 支持的并发模型（Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307713"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支持的并发模型（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序支持*只读并发*。 应用程序可以使用 SQL_CONCUR_READ_ONLY SQL_CONCURRENCY 选项调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 。  
  
 有关详细信息，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>只读并发  
 无法更新游标。  
  
## <a name="row-versioning"></a>行版本控制 (row versioning)  
 实质上是时间戳支持，在这种情况下，行版本在更新时进行比较。
