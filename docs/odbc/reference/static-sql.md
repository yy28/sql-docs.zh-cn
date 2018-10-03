---
title: 静态 SQL |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cd82e2c3c44f05a27e9d14442d8d0fb58e1986cc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849135"
---
# <a name="static-sql"></a>静态 SQL
嵌入式的 SQL 中所示[嵌入式 SQL 示例](../../odbc/reference/embedded-sql-example.md)称为静态 SQL。 由于在程序中的 SQL 语句都是静态的; 因此，称为静态 SQL也就是说，它们不会更改每次运行该程序。 如前一部分中所述，这些语句进行编译时编译的程序的其余部分。  
  
 静态 SQL 适用于很多情况下，可以在程序设计时可以为其确定数据访问任何应用程序中使用。 例如，订单输入程序始终使用同一个语句插入新订单和航空订票系统始终使用相同的语句席位将状态从可用于保留更改。 每个这些语句会通过主机变量; 使用通用化不同的值，可插入销售订单，并可以保留不同席位。 由于此类语句可以是硬编码在程序中，此类程序具有的优势在于语句需要分析、 验证，并在编译时只有一次优化。 这会导致相对较快的代码。
