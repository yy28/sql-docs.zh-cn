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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107519"
---
# <a name="sql-conformance-levels"></a>SQL 一致性级别
通过调用返回的值指示驱动程序支持的 SQL-92 语法级别**SQLGetInfo** SQL_SQL_CONFORMANCE 信息类型。 这表示该驱动程序是否符合 SQL-92 中定义的项、 FIPS 过渡、 中间，或完全级别。  
  
 所有 ODBC 驱动程序必须都支持中所述的最小 SQL 语法[SQL 最低语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)附录 c： 驱动器中SQL 语法。 此语法是 SQL-92 的入门级的子集。 驱动程序可能支持其他 SQL 和都符合标准的 SQL-92 条目、 中级或完整的级别，或 FIPS 127-2 过渡级别。 到给定级别的 SQL-92 或 FIPS 127-2 遵从的驱动程序可以在任何更高级别支持其他功能，但可能不是完全符合该级别。 若要确定是否支持某一功能，应用程序应调用**SQLGetInfo**与相应的信息类型。 SQL 功能的一致性级别所述的相应的信息类型。 (请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。)
