---
title: "SQL 一致性级别 |Microsoft 文档"
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
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d397eef2bec5e803cca97f05d009708273a05473
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="sql-conformance-levels"></a>SQL 一致性级别
由通过调用返回的值指示的驱动程序支持的 SQL 92 语法级别**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 这指示该驱动程序是否符合 SQL 92 中定义的项、 FIPS 过渡、 中间，或完全级别。  
  
 所有 ODBC 驱动程序必须都支持的最小的 SQL 语法中所述[SQL 最小语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)附录 c: SQL 语法中。 此语法是 SQL 92 入门级的子集。 驱动程序可能支持其他 SQL 和其符合标准的 SQL 92 条目、 中级或完全级别，或 FIPS 127 2 过渡级别。 给定级别的 SQL 92 或经过了 FIPS 127 2 到符合的驱动程序可以支持任何更高级别中的其他功能，但可能不是完全符合该级别。 若要确定是否支持的功能，应用程序应调用**SQLGetInfo**与相应的信息类型。 SQL 功能的一致性级别是在相应的信息类型中所述。 (请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。)
