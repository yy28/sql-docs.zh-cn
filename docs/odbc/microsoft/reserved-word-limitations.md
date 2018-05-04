---
title: 保留 Word 限制 |Microsoft 文档
ms.custom: ''
ms.date: 05/01/2018
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
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ed42f083-c9e8-4ee4-9d64-d879bf955c78
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac61a7aa818ef3593fddc630d5027fbf7e4aa211
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="reserved-keyword-limitations"></a>保留的关键字限制

避免使用与你的 SQL 表或相关的对象中的标识符的任何 ODBC 保留关键字。 如果独特的情况下出现其中必须将保留的关键字用作标识符，必须使用一对环绕标识符*backticks* （'）。 另一个名称*反撇号*是*反引号*。

保留的关键字限制也适用于任何速记形式的保留关键字。

ODBC 保留关键字的列表位于：

- [ODBC 保留关键字](https://docs.microsoft.com/sql/odbc/reference/appendixes/reserved-keywords)。

- 在*ODBC 程序员参考指南*，请参阅[附录 c: SQL 语法](https://docs.microsoft.com/sql/odbc/reference/appendixes/appendix-c-sql-grammar)。

