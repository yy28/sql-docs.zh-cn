---
title: 是一个结果集，创建？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a7222a9dcbbf7c979dd46ff554fab5988bcfada4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="was-a-result-set-created"></a>是一个结果集，创建？
在大多数情况下，应用程序程序员知道他们的应用程序执行的语句是否将创建一个结果集。 如果应用程序使用硬编码 SQL 语句将程序员编写的这种情况。 它通常是这种情况，当应用程序在运行时构造 SQL 语句时： 程序员可以轻松地将标记的代码是否**选择**语句或**插入**正在语句构造。 在少数情况下，程序员可能无法知道是否语句将创建一个结果集。 这是如果应用程序为提供一种用户输入并执行的 SQL 语句为 true。 此外，当应用程序构造在运行时执行过程的语句时对它也是如此。  
  
 在这种情况下，在应用程序调用**SQLNumResultCols**以确定结果集中的列数。 如果这是 0，语句未创建结果集;如果它是其他任何数字，该语句未创建结果集。  
  
 应用程序可以调用**SQLNumResultCols**次后准备或执行该语句。 但是，因为某些数据源不能轻松地描述将创建的已准备的语句的结果集，性能将会降低如果**SQLNumResultCols**准备语句之后但在执行之前调用。  
  
 某些数据源还支持确定的 SQL 语句返回结果集中的行数。 为此，请在应用程序调用**SQLRowCount**。 完全行计数所表示的内容由 （具体取决于游标的类型） SQL_DYNAMIC_CURSOR_ATTRIBUTES2、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 选项的设置指示返回通过调用**SQLGetInfo**。 此位掩码指示了对于每种游标类型返回的行计数是否完全相同的、 近似，或根本不可用。 适用于静态行计数还是通过所做的更改会影响键集驱动游标**SQLBulkOperations**或**SQLSetPos**，或通过定位的 update 或 delete 语句，依赖于其他位返回前面列出的相同选项自变量。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
