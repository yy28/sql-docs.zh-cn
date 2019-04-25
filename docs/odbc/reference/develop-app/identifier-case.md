---
title: 标识符的大小写 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6445cffd5faa8b825c81ec729d7b28c90e14a7b3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62447819"
---
# <a name="identifier-case"></a>标识符大小写
在 SQL 语句和目录函数自变量中，标识符和带引号的标识符可以是区分大小写或不是，该应用程序可以确定通过调用**SQLGetInfo** SQL_IDENTIFIER_CASE 和 SQL_QUOTED_IDENTIFIER_CASE 选项。  
  
 每个这些选项都有四个可能的返回值： 一个声明的标识符或带引号的标识符的大小写不敏感和三个指示不敏感。 不区分大小写的三个值进一步描述用例在系统目录中存储标识符。 如何在系统目录中存储的标识符是相关仅出于显示目的，例如当应用程序显示目录函数; 的结果它不会更改标识符区分大小的写。
