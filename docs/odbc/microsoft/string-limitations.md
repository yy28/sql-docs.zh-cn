---
description: 字符串限制
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
ms.openlocfilehash: c21d86a3c626ced52c6b7915d3cfbd9322fb596e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449129"
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为65000个字符。  
  
 使用 Microsoft Access 驱动程序时，仅支持 (带有单引号的 SQL-92 字符串常量，而不支持双引号) 。  
  
 不能在字符串中使用 ( # A0) 的管道字符，无论该字符是否括在引号中。  
  
 为了实现最大互操作性，应用程序应在参数中传递字符串，而不是传递带引号的字符串。
