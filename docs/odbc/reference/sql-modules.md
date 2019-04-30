---
title: SQL 模块 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c116878049c4f6a8f36e988731ab641e03c6d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232779"
---
# <a name="sql-modules"></a>SQL 模块
将 SQL 语句发送到 DBMS 的第二个方法是通过模块。 简单地说，模块包含的一组过程，从主机编程语言调用。 每个过程包含单个 SQL 语句，且数据将传递到和从过程参数。  
  
 模块可以看作链接到应用程序代码的对象库。 但是，确切过程和应用程序的其余部分如何链接是依赖于实现的。 例如，过程无法为对象代码编译和链接直接到应用程序代码可以编译并存储在上的 DBMS 和调用来访问计划标识符放在应用程序代码中，或它们无法在运行时解释。  
  
 模块的主要优点是它们完全隔离的编程语言中的 SQL 语句。 从理论上讲，它应该可以更改而无需更改另一个，只需将它们重新链接。
