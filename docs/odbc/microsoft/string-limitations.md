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
manager: craigg
ms.openlocfilehash: 003cd318d6db54c7547375219805c63cfc4ce249
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668375"
---
# <a name="string-limitations"></a>字符串限制
SQL 语句字符串的最大长度为 65,000 个字符。  
  
 使用 Microsoft Access 驱动程序时，只有 SQL-92 （用单引号，没有两个双引号） 的字符串常量支持。  
  
 竖线字符 (&#124;) 指示字符是否用用后引号引起来或不能在字符串中使用。  
  
 对于最大互操作性，应用程序应将字符串参数，而不是传递带引号的字符串。
