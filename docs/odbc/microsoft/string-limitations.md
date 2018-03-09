---
title: "字符串限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2a805c4a0f98b394929f5b5a7b21613eac728533
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为 65000 个字符。  
  
 当使用 Microsoft Access 驱动程序时，支持仅 （具有单个引号引起来，没有两个双引号） 的 SQL 92 字符串常量。  
  
 管道字符 (&#124;) 不能在字符串内，是否字符用引号括起来后与否。  
  
 对于最大互操作性，应用程序应将字符串传递在参数中，而不是传递带引号的字符串。
