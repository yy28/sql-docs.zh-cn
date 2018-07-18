---
title: 静态 SQL |Microsoft 文档
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
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ff2144ae69c48098324bc0b97ca9c33d5159adc3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915173"
---
# <a name="static-sql"></a>静态 SQL
中所示嵌入式的 SQL[嵌入式 SQL 示例](../../odbc/reference/embedded-sql-example.md)称为静态 SQL。 在程序中的 SQL 语句是静态的; 因为，称为静态 SQL也就是说，它们不会更改每次运行该程序。 如前一部分中所述，这些语句进行编译的程序的其余部分时，编译。  
  
 适用于许多情况下，静态 SQL，可以在程序设计时可以为其确定数据访问任何应用程序中使用。 例如，订单条目程序始终使用同一语句以将新的订单，插入和航空订票系统始终使用相同的语句的座位将状态从可用于保留更改。 上述每个语句将通过主机变量; 使用通用化不同的值可以插入销售订单中，并且可以保留不同的座位数。 因为这些语句可以将其硬编码在程序中，此类程序有一些优点，语句需要分析、 验证，并且在编译时一次优化。 这会导致相对较快的代码。
