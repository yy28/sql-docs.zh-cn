---
title: 数值 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], numeric data types
- numeric data type [ODBC], literals
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 9dc23656-61e1-4b62-a07f-64ab716e45d2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 994bbed6ed3454c6213b16faabf5a0de7eeabbf9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299847"
---
# <a name="numeric-literals"></a>数值
当数值数据值存储在字符串中时，将使用数字文本。 若要将数字 SQL 数据转换为 SQL_C_CHAR 字符串，或者将数字 C 数据转换为 SQL_CHAR 或 SQL_VARCHAR 字符串，请使用数字文本语法来指定目标中存储的内容。 若要将存储为 SQL_C_CHAR 字符串的数字转换为数值 SQL 数据，或者将数字存储为数字 C 数据的 SQL_CHAR 字符串，请使用此语法来验证源中存储的内容。  
  
 数字文本应符合附录 C： SQL 句法部分的[数字文本语法](../../../odbc/reference/appendixes/numeric-literal-syntax.md)中定义的语法。  
  
 本部分包含以下主题。  
  
-   [转换规则](../../../odbc/reference/appendixes/rules-for-conversions.md)  
  
-   [重写数字数据类型的默认精度和小数位数](../../../odbc/reference/appendixes/overriding-default-precision-and-scale-for-numeric-data-types.md)
