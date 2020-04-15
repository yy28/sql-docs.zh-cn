---
title: 字符串限制 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f81ff3da882095a0a6c41bb5061addd497a5d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306058"
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为 65，000 个字符。  
  
 使用 Microsoft Access 驱动程序时，仅支持 SQL-92 字符串常量（带有单引号，而不是双引号）。  
  
 无论该字符是否包含在后引号中，都不能在字符串中使用管道字符（&#124;）。  
  
 为了达到最大的互操作性，应用程序应传递参数中的字符串，而不是传递引号字符串。
