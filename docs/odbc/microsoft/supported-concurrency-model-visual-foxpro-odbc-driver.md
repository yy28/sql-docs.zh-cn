---
title: 支持的并发模型 （Visual FoxPro ODBC 驱动程序） |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080694"
---
# <a name="supported-concurrency-model-visual-foxpro-odbc-driver"></a>支持的并发模型（Visual FoxPro ODBC 驱动程序）
Visual FoxPro ODBC 驱动程序支持*只读并发*。 你的应用程序可以调用[SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) SQL_CONCUR_READ_ONLY SQL_CONCURRENCY 选项。  
  
 有关详细信息，请参阅[ODBC 程序员参考](../../odbc/reference/odbc-programmer-s-reference.md)。  
  
## <a name="read-only-concurrency"></a>只读并发  
 不能更新游标。  
  
## <a name="row-versioning"></a>行版本控制 (row versioning)  
 实质上是时间戳的支持中的行版本相比在更新时。
