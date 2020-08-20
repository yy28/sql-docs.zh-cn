---
description: SQL 模块
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39739ed5469b791cd0faf3df3946bebeb5d21761
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499640"
---
# <a name="sql-modules"></a>SQL 模块
向 DBMS 发送 SQL 语句的第二种方法是通过模块。 简而言之，模块包含一组过程，这些过程是从主机编程语言中调用的。 每个过程都包含单个 SQL 语句，并通过参数将数据传递给和。  
  
 模块可被视为链接到应用程序代码的对象库。 但确切地说，应用程序和应用程序的其余部分是依赖实现的。 例如，可以将这些过程编译到对象代码中，并直接链接到应用程序代码，它们可以编译并存储在 DBMS 上，并可以调用来访问应用程序代码中放置的计划标识符，也可以在运行时解释它们。  
  
 模块的主要优点是它们从编程语言中完全分离 SQL 语句。 理论上，应该可以更改一个，而无需更改另一个，而只需重新链接它们即可。
