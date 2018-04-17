---
title: 静态 SQL |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
ms.workload: Inactive
ms.openlocfilehash: 392cf843734bcc668c88f6408227b20df97d43ae
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="static-sql"></a>静态 SQL
中所示嵌入式的 SQL[嵌入式 SQL 示例](../../odbc/reference/embedded-sql-example.md)称为静态 SQL。 在程序中的 SQL 语句是静态的; 因为，称为静态 SQL也就是说，它们不会更改每次运行该程序。 如前一部分中所述，这些语句进行编译的程序的其余部分时，编译。  
  
 适用于许多情况下，静态 SQL，可以在程序设计时可以为其确定数据访问任何应用程序中使用。 例如，订单条目程序始终使用同一语句以将新的订单，插入和航空订票系统始终使用相同的语句的座位将状态从可用于保留更改。 上述每个语句将通过主机变量; 使用通用化不同的值可以插入销售订单中，并且可以保留不同的座位数。 因为这些语句可以将其硬编码在程序中，此类程序有一些优点，语句需要分析、 验证，并且在编译时一次优化。 这会导致相对较快的代码。
