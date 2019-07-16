---
title: 字符串限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7faab41bd52397ac0d352e04a9ec153571e93f1e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67948764"
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为 65,000 个字符。  
  
 使用 Microsoft Access 驱动程序时，只有 SQL-92 （用单引号，没有两个双引号） 的字符串常量支持。  
  
 竖线字符 (&#124;) 指示字符是否用用后引号引起来或不能在字符串中使用。  
  
 对于最大互操作性，应用程序应将字符串参数，而不是传递带引号的字符串。
