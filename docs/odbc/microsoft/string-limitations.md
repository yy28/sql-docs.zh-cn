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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67948764"
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为65000个字符。  
  
 使用 Microsoft Access 驱动程序时，仅支持 SQL-92 字符串常量（带有单引号，而不是双引号）。  
  
 在字符串中不能使用竖线字符（&#124;），无论该字符是否括在引号中。  
  
 为了实现最大互操作性，应用程序应在参数中传递字符串，而不是传递带引号的字符串。
