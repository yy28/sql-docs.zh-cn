---
title: SQL 语句的互操作性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4ead7cf96ada6d6055bc676ecf4610f2cf4c8f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622475"
---
# <a name="interoperability-of-sql-statements"></a>SQL 语句的互操作性
应用程序的其余部分，如 SQL 语句可以是可互操作或特定于 DBMS 的。 和需要的应用程序的其余部分，如是如何可互操作的 SQL 语句的选择取决于应用程序的类型。 自定义应用程序不太可能使用可互操作的 SQL 语句，因为它们通常设计为利用一个或可能是两个 Dbms 的功能。 通用应用程序使用可互操作的 SQL 语句，因为它们用于处理各种 Dbms。 和垂直应用程序通常在某个位置之间，要求苛刻的特定级别的功能，但以其他方式使用可互操作的 SQL 语句。  
  
 本部分包含以下主题。  
  
-   [选择 SQL 语法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [构造交互 SQL 语句](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
