---
title: SQL 模块 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280419"
---
# <a name="sql-modules"></a>SQL 模块
向 DBMS 发送 SQL 语句的第二种技术是通过模块。 简而言之，模块由一组过程组成，这些过程从主机编程语言调用。 每个过程都包含一个 SQL 语句，数据通过参数传入过程并从过程传递。  
  
 模块可以视为链接到应用程序代码的对象库。 但是，过程和应用程序的其余部分的关联方式与实现有关。 例如，过程可以编译为对象代码并直接链接到应用程序代码，可以编译并存储在 DBMS 上，并调用应用程序代码中放置的访问计划标识符，也可以在运行时对其进行解释。  
  
 模块的主要优点是它们将 SQL 语句与编程语言完全分开。 从理论上讲，应该可以改变一个而不改变另一个，只是重新链接他们。
