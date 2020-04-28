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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f81ff3da882095a0a6c41bb5061addd497a5d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306058"
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为65000个字符。  
  
 使用 Microsoft Access 驱动程序时，仅支持 SQL-92 字符串常量（带有单引号，而不是双引号）。  
  
 在字符串中不能使用竖线字符（&#124;），无论该字符是否括在引号中。  
  
 为了实现最大互操作性，应用程序应在参数中传递字符串，而不是传递带引号的字符串。
