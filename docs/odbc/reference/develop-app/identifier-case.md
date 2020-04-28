---
title: 标识符大小写 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300147"
---
# <a name="identifier-case"></a>标识符大小写
在 SQL 语句和目录函数参数中，标识符和带引号的标识符可以区分大小写，应用程序可以通过使用 SQL_IDENTIFIER_CASE 和 SQL_QUOTED_IDENTIFIER_CASE 选项调用**SQLGetInfo**来确定。  
  
 其中每个选项都有四个可能的返回值：一个声明标识符或带引号的标识符的大小写，三个表示它是不敏感的。 这三个不区分大小写的值会进一步描述标识符存储在系统目录中的情况。 标识符在系统目录中的存储方式仅适用于显示目的，例如当应用程序显示目录函数的结果时。它不会更改标识符的区分大小写。
