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
ms.openlocfilehash: 2e6d053e4d2a5520432c4c1debbafb35fdb17bc4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68016738"
---
# <a name="static-sql"></a>静态 SQL
嵌入的 sql[示例](../../odbc/reference/embedded-sql-example.md)中所示的嵌入式 sql 称为 "静态 sql"。 它被称为静态 SQL，因为程序中的 SQL 语句是静态的;也就是说，每次运行程序时它们都不会更改。 如上一节所述，编译程序的其余部分时，将编译这些语句。  
  
 静态 SQL 在很多情况下都可以很好地工作，并且可以在任何可在程序设计时为其确定数据访问权限的应用程序中使用。 例如，订单输入程序始终使用同一语句插入新订单，并且航空公司预订系统始终使用同一语句将座位的状态从 "可用" 更改为 "已保留"。 其中每个语句都将通过使用主机变量来通用化;可以在销售订单中插入不同的值，并且可以保留不同的座位。 由于此类语句可以在程序中进行硬编码，因此此类程序的优点是，在编译时，语句只需进行分析、验证和优化一次。 这会导致代码相对较快。
