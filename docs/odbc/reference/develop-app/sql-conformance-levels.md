---
title: SQL 一致性级别 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 875330ac78588566b4b1c212f7a65d2841127a61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301378"
---
# <a name="sql-conformance-levels"></a>SQL 一致性级别
驱动程序支持的 SQL-92 语法级别由调用**SQLGetInfo**返回的值（具有SQL_SQL_CONFORMANCE信息类型）指示。 这指示驱动程序是否符合 SQL-92 中定义的入口、FIPS 过渡、中间或完整级别。  
  
 所有 ODBC 驱动程序都必须支持附录 C：SQL 语法中的[SQL 最小语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md)中描述的最小 SQL 语法。 此语法是 SQL-92 条目级别的子集。 驱动程序可能支持其他 SQL，并且符合 SQL-92 输入、中间或完整级别，或符合 FIPS 127-2 过渡级别。 符合给定级别的 SQL-92 或 FIPS 127-2 的驱动程序可以支持任何较高级别的其他功能，但尚未完全符合该级别。 要确定是否支持某项功能，应用程序应使用适当的信息类型调用**SQLGetInfo。** SQL 功能的一致性级别在相应的信息类型中描述。 （请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
