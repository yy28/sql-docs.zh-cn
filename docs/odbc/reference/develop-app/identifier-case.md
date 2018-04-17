---
title: 标识符的大小写 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- identifiers [ODBC], case
- interoperability of SQL statements [ODBC], identifier case
ms.assetid: ee8a31aa-389d-4dd1-bfa9-547f6b50bc70
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 122f4dfdfab25f246858b36f7753413d25f2eea4
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="identifier-case"></a>标识符的大小写
在 SQL 语句和目录函数自变量中，标识符和带引号的标识符可以是区分大小写或不是，该应用程序可以确定通过调用**SQLGetInfo** SQL_IDENTIFIER_CASE 与 SQL_QUOTED_IDENTIFIER_CASE 选项。  
  
 其中每个选项具有四个可能的返回值： 一个指出标识符或带引号的标识符的大小写敏感和三个，则表明它不属于最敏感。 不区分大小写的三个值进一步描述用例标识符在系统目录中的存储。 标识符在系统目录中的存储方式是仅用于显示目的，如应用程序时显示的目录函数; 结果相关它不会更改标识符区分大小的写。
