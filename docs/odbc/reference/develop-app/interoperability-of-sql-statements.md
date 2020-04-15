---
title: SQL 语句的互操作性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3d7a76c67096d2e76fe1cd3d4b15f73122699e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302798"
---
# <a name="interoperability-of-sql-statements"></a>SQL 语句的互操作性
与应用程序的其余部分一样，SQL 语句可以互操作或特定于 DBMS。 与应用程序的其余部分一样，选择可互操作的 SQL 语句取决于应用程序的类型。 自定义应用程序不太可能使用可互操作的 SQL 语句，因为它们通常旨在利用一个或两个 DBMS 的功能。 通用应用程序使用可互操作的 SQL 语句，因为它们旨在处理各种 DBMS。 垂直应用程序通常介于两者之间，需要一定的功能级别，但使用可互操作的 SQL 语句。  
  
 本部分包含以下主题。  
  
-   [选择 SQL 语法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [构造交互 SQL 语句](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
