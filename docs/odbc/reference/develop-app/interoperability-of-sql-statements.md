---
title: "SQL 语句的互操作性 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ebbf617702162e2f1de9920375cfe0cb51246300
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="interoperability-of-sql-statements"></a>SQL 语句的互操作性
应用程序的其余部分，如 SQL 语句可以是可互操作或特定于 DBMS 的。 和需要应用程序的其余部分，如是如何可互操作的 SQL 语句的选择取决于应用程序的类型。 自定义应用程序不太可能使用可互操作的 SQL 语句，因为它们通常设计为利用一个或两个可能的 Dbms 的功能。 通用应用程序使用可互操作的 SQL 语句，因为它们被设计用于与各种 Dbms。 并垂直应用程序通常归的某处之间，要求严苛的特定级别的功能，但以其他方式使用可互操作的 SQL 语句。  
  
 本部分包含以下主题。  
  
-   [选择 SQL 语法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [构造交互 SQL 语句](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
