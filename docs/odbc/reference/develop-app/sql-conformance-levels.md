---
title: SQL 一致性级别 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7862b2e3a86c6d98a51c73ecb470d59bcfe29dc9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107519"
---
# <a name="sql-conformance-levels"></a>SQL 一致性级别
驱动程序支持的 SQL-92 语法级别由对 SQL_SQL_CONFORMANCE 信息类型的**SQLGetInfo**的调用返回的值指示。 这表明驱动程序是否符合 SQL-92 中定义的条目、FIPS 过渡、中间或全部级别。  
  
 所有 ODBC 驱动程序都必须支持附录 C： SQL 语法中的[Sql 最低语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)中所述的最低 sql 语法。 此语法是 SQL-92 的条目级别的子集。 驱动程序可以支持其他 SQL，并符合 SQL-92 项、中间或完整级别，或符合 FIPS 127-2 过渡级别。 符合给定级别的 SQL-92 或 FIPS 127-2 的驱动程序可以支持任何更高级别中的其他功能，但并不完全符合该级别。 若要确定功能是否受支持，应用程序应使用适当的信息类型调用**SQLGetInfo** 。 相应的信息类型中描述了 SQL 功能的一致性级别。 （请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。）
