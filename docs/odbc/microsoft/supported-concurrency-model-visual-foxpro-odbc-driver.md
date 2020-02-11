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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 597d1022fa6946e0ae768cb9600a3f4534c67a25
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68080694"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支持的并发模型（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序支持*只读并发*。 应用程序可以使用 SQL_CONCUR_READ_ONLY SQL_CONCURRENCY 选项调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) 。  
  
 有关详细信息，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>只读并发  
 无法更新游标。  
  
## <a name="row-versioning"></a>行版本控制 (row versioning)  
 实质上是时间戳支持，在这种情况下，行版本在更新时进行比较。
