---
title: SQL 语句的互操作性 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 205fd667e8891ba0bab0283c1d112af9d608423b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909862"
---
# <a name="interoperability-of-sql-statements"></a>SQL 语句的互操作性
应用程序的其余部分，如 SQL 语句可以是可互操作或特定于 DBMS 的。 和需要应用程序的其余部分，如是如何可互操作的 SQL 语句的选择取决于应用程序的类型。 自定义应用程序不太可能使用可互操作的 SQL 语句，因为它们通常设计为利用一个或两个可能的 Dbms 的功能。 通用应用程序使用可互操作的 SQL 语句，因为它们被设计用于与各种 Dbms。 并垂直应用程序通常归的某处之间，要求严苛的特定级别的功能，但以其他方式使用可互操作的 SQL 语句。  
  
 本部分包含以下主题。  
  
-   [选择 SQL 语法](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [构造交互 SQL 语句](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
