---
description: SQL 一致性级别
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 525cda9094213e6decf30643c23a7db623511e14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499800"
---
# <a name="sql-conformance-levels"></a>SQL 一致性级别
驱动程序支持的 SQL-92 语法级别由对 SQL_SQL_CONFORMANCE 信息类型的 **SQLGetInfo** 的调用返回的值指示。 这表明驱动程序是否符合 SQL-92 中定义的条目、FIPS 过渡、中间或全部级别。  
  
 所有 ODBC 驱动程序都必须支持附录 C： SQL 语法中的 [Sql 最低语法](../../../odbc/reference/appendixes/sql-minimum-grammar.md) 中所述的最低 sql 语法。 此语法是 SQL-92 的条目级别的子集。 驱动程序可以支持其他 SQL，并符合 SQL-92 项、中间或完整级别，或符合 FIPS 127-2 过渡级别。 符合给定级别的 SQL-92 或 FIPS 127-2 的驱动程序可以支持任何更高级别中的其他功能，但并不完全符合该级别。 若要确定功能是否受支持，应用程序应使用适当的信息类型调用 **SQLGetInfo** 。 相应的信息类型中描述了 SQL 功能的一致性级别。  (参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函数说明。 ) 
