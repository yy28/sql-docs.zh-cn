---
title: 带引号的标识符 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0a81237eddd4836394cc9797a79690ba4b49a35
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861639"
---
# <a name="quoted-identifiers"></a>带引号的标识符
在 SQL 语句，其中包含特殊字符或匹配关键字的标识符必须括在*标识符引号字符*; 在此类字符中包含的标识符称为*带引号的标识符*(也称为*分隔的标识符*SQL-92 中)。 例如，在下面的示例引用 Accounts Payable 标识符**选择**语句：  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 标识符引起来的原因是为了使语句可解析。 例如，如果 Accounts Payable 不带引号在前一个语句中，分析器将假定没有两个表，帐户和帐款，并返回语法错误，不是用逗号分隔。 引号字符标识符是特定于驱动程序，在使用中的 SQL_IDENTIFIER_QUOTE_CHAR 选项检索**SQLGetInfo**。 通过 SQL_SPECIAL_CHARACTERS 和 SQL_KEYWORDS 的选项中检索的特殊字符和的关键字的列表**SQLGetInfo**。  
  
 为了安全起见，可互操作应用程序通常引用除伪列，如行 ID 列在 Oracle 中的所有标识符。 **SQLSpecialColumns**返回伪列的列表。 此外，如果有特殊字符的对象名称中可以出现的位置的特定于应用程序的限制，是最佳的可互操作应用程序不应在这些位置中使用特殊字符。
