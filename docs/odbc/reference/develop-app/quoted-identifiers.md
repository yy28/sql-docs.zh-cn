---
title: 引用的标识符 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282000"
---
# <a name="quoted-identifiers"></a>带引号的标识符
在 SQL 语句中，包含特殊字符或匹配关键字的标识符必须包含在*标识符报价字符*中;这些字符中包含的标识符称为*引号标识符*（也称为 SQL-92 中的*分隔标识符*）。 例如，应付帐款标识符在以下**SELECT**语句中引用：  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 引用标识符的原因是使语句可解析。 例如，如果上一个语句中未引用应付帐款，则解析器将假定有两个表，即"应付帐款"和"应付帐款"，并返回一个语法错误，即它们未用逗号分隔。 标识符报价字符特定于驱动程序，并且使用**SQLGetInfo**中的SQL_IDENTIFIER_QUOTE_CHAR选项进行检索。 使用**SQLGetInfo**中SQL_SPECIAL_CHARACTERS和SQL_KEYWORDS选项检索特殊字符和关键字的列表。  
  
 为了安全起见，可互操作的应用程序通常引用除伪列以外的所有标识符，例如 Oracle 中的 ROWID 列。 **SQL 特殊列**返回伪列的列表。 此外，如果存在特殊字符在对象名称中显示的位置，则最好对可互操作的应用程序在这些位置不使用特殊字符。
