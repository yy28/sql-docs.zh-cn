---
title: 保留字限制 |Microsoft Docs
ms.custom: ''
ms.date: 05/01/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c884d8594c3c4511bed0e24f9b3dd43092176b4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67988024"
---
# <a name="reserved-keyword-limitations"></a>保留关键字限制

避免在 SQL 表或相关对象中使用任何 ODBC 保留关键字作为标识符。 如果需要将保留关键字用作标识符，则必须使用*反撇号*（'）将标识符括起来。 *反撇号*的另一个名称是*后退引号*。

保留关键字限制还适用于保留关键字的任何简写形式。

ODBC 保留关键字的列表位于：

- [ODBC 保留关键字](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)。

- 有关*ODBC 程序员参考指南*，请参阅[附录 C： SQL 语法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)。

