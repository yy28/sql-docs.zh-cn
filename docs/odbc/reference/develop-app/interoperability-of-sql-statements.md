---
description: SQL 语句的互操作性
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 64127e97adf08c3de9f391810a259a3b7045bdc1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476619"
---
# <a name="interoperability-of-sql-statements"></a>SQL 语句的互操作性
与应用程序的其余部分一样，SQL 语句可以互操作或 DBMS 特定的。 与应用程序的其余部分一样，可交互的 SQL 语句如何需要取决于应用程序的类型。 自定义应用程序不太可能使用可互操作的 SQL 语句，因为它们通常设计为利用一个或可能两个 Dbms 的功能。 一般应用程序使用可互操作的 SQL 语句，因为它们设计为适用于各种 Dbms。 和垂直应用程序通常在两者之间，要求一定级别的功能，但使用可互操作的 SQL 语句。  
  
 本部分包含以下主题。  
  
-   [选择 SQL 语法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [构造交互 SQL 语句](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
