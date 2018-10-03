---
title: 是否创建了一个结果集？ | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], determining if created
ms.assetid: 4a83b8cb-2d57-4e64-b497-80bd587ee1f9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db287e729678f54aaf637950c89c724724678f08
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47650295"
---
# <a name="was-a-result-set-created"></a>是否创建了一个结果集？
在大多数情况下，应用程序程序员知道其应用程序执行的语句是否将创建一个结果集。 如果应用程序使用硬编码的 SQL 语句将程序员编写的这是这种情况。 它通常是这种情况，应用程序在运行时构造 SQL 语句时： 编程人员可以轻松地添加标记的代码是否**选择**语句或**插入**语句构造。 在少数情况下，程序员可能不知道语句是否将创建一个结果集。 这是如果应用程序提供了一种方法为用户输入和执行 SQL 语句，则返回 true。 此外，应用程序构造的语句在运行时执行过程时对它也是如此。  
  
 在这种情况下，应用程序调用**SQLNumResultCols**以确定结果集中的列数。 如果这是 0，该语句未创建结果集;如果是其他任何数字，该语句未创建结果集。  
  
 应用程序可以调用**SQLNumResultCols**次后在准备或执行该语句。 但是，因为某些数据源不能轻松地描述将创建的预定义语句的结果集，性能会降低如果**SQLNumResultCols**语句已准备就绪后，但它在执行之前调用。  
  
 某些数据源还支持确定的 SQL 语句返回结果集中的行数。 若要执行此操作，应用程序调用**SQLRowCount**。 完全行计数表示的内容由 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、 SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 选项 （具体取决于游标的类型） 的设置指示返回通过调用**SQLGetInfo**。 此位掩码指示为每个游标类型返回的行计数是否准确、 近似，或根本不提供。 适用于静态行计数，还是通过所做的更改会影响由键集驱动的游标**SQLBulkOperations**或**SQLSetPos**，或通过定位的 update 或 delete 语句，依赖于其他位返回前面列出的相同选项参数。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
