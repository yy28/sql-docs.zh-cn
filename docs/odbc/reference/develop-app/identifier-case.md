---
title: 标识符案例 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 940d96ece6b2c344fa02e0daadd6248270f4d19e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300147"
---
# <a name="identifier-case"></a>标识符大小写
在 SQL 语句和目录函数参数中，标识符和引号标识符可以是区分大小写或不，应用程序可以通过使用SQL_IDENTIFIER_CASE和SQL_QUOTED_IDENTIFIER_CASE选项调用**SQLGetInfo**来确定。  
  
 每个选项都有四个可能的返回值：一个表示标识符或引号标识符大小写是敏感的，三个表示它不敏感。 不区分大小写的三个值进一步描述了标识符存储在系统目录中的情况。 标识符在系统目录中的存储方式仅与显示目的相关，例如当应用程序显示目录函数的结果时;当应用程序显示目录函数的结果时，如何将标识符存储在系统目录中。它不更改标识符的区分大小写。
