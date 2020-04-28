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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 351d1c6a34413b385bd76dfebb009b34c4c0f150
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280419"
---
# <a name="sql-modules"></a>SQL 模块
向 DBMS 发送 SQL 语句的第二种方法是通过模块。 简而言之，模块包含一组过程，这些过程是从主机编程语言中调用的。 每个过程都包含单个 SQL 语句，并通过参数将数据传递给和。  
  
 模块可被视为链接到应用程序代码的对象库。 但确切地说，应用程序和应用程序的其余部分是依赖实现的。 例如，可以将这些过程编译到对象代码中，并直接链接到应用程序代码，它们可以编译并存储在 DBMS 上，并可以调用来访问应用程序代码中放置的计划标识符，也可以在运行时解释它们。  
  
 模块的主要优点是它们从编程语言中完全分离 SQL 语句。 理论上，应该可以更改一个，而无需更改另一个，而只需重新链接它们即可。
