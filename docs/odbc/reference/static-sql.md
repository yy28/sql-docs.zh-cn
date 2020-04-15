---
title: 静态 SQL |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55710d8ea734cba86ae5e4daa725f75e94e65a64
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279899"
---
# <a name="static-sql"></a>静态 SQL
[嵌入式 SQL 示例中](../../odbc/reference/embedded-sql-example.md)显示的嵌入式 SQL 称为静态 SQL。 它被称为静态 SQL，因为程序中的 SQL 语句是静态的;也就是说，它们不会在每次运行程序时更改。 如上一节所述，这些语句是在编译程序的其余部分时编译的。  
  
 静态 SQL 在许多情况下工作良好，可用于可在程序设计时确定数据访问的任何应用程序中使用。 例如，订单输入程序始终使用相同的语句来插入新订单，航空公司预订系统始终使用相同的语句将座位的状态从可用更改为预留。 这些语句中的每一个都将通过使用宿主变量进行概括;可以在销售订单中插入不同的值，并可以保留不同的席位。 由于此类语句可以在程序中硬编码，因此此类程序的优点是，在编译时，语句只需分析、验证和优化一次。 这会导致代码相对快速。
