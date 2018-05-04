---
title: 字符串限制 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd397b02f72a9962e4fe87683141fa98f81cfbdc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为 65000 个字符。  
  
 当使用 Microsoft Access 驱动程序时，支持仅 （具有单个引号引起来，没有两个双引号） 的 SQL 92 字符串常量。  
  
 管道字符 (&#124;) 是否字符用引号括起来后是否不在字符串中使用。  
  
 对于最大互操作性，应用程序应将字符串传递在参数中，而不是传递带引号的字符串。
