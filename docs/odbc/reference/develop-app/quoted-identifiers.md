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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282000"
---
# <a name="quoted-identifiers"></a>带引号的标识符
在 SQL 语句中，包含特殊字符或匹配关键字的标识符必须用*标识符引号字符*括起来。括在此类字符中的标识符称为*带引号的标识符*（也称为 SQL-92 中的*分隔标识符*）。 例如，以下**SELECT**语句中的帐户应付帐款标识符用引号引起来：  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 引用标识符的原因是为了使语句不可解析。 例如，如果在上一条语句中未将应付帐款括在引号中，则分析器会假设有两个表、帐户和应付，并返回未用逗号分隔的语法错误。 标识符引号字符是特定于驱动程序的，并在**SQLGetInfo**中用 SQL_IDENTIFIER_QUOTE_CHAR 选项来检索。 将用**SQLGetInfo**中的 SQL_SPECIAL_CHARACTERS 和 SQL_KEYWORDS 选项检索特殊字符和关键字的列表。  
  
 为安全起见，可互操作的应用程序通常会将所有标识符（对于伪列除外）括起来，如 Oracle 中的 ROWID 列。 **SQLSpecialColumns**返回伪列列表。 此外，如果有特定于应用程序的限制，在对象名称中可以出现特殊字符，则它最适用于可互操作的应用程序，而不是在这些位置中使用特殊字符。
