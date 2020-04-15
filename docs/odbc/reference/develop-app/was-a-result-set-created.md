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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c171a154dd16a291c5dbe1dcade8c01ea95fb084
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294545"
---
# <a name="was-a-result-set-created"></a>是否创建了一个结果集？
在大多数情况下，应用程序程序员知道应用程序执行的语句是否会创建结果集。 如果应用程序使用程序员编写的硬编码 SQL 语句，则就是这种情况。 通常，当应用程序在运行时构造 SQL 语句时，通常就是这种情况：程序员可以轻松地包含标记正在构造**SELECT**语句还是**INSERT**语句的代码。 在某些情况下，程序员不可能知道语句是否会创建结果集。 如果应用程序为用户提供了一种输入和执行 SQL 语句的方法，则为这种情况为 1。 当应用程序在运行时构造语句以执行过程时也是如此。  
  
 在这种情况下，应用程序调用**SQLNumResultCols**以确定结果集中的列数。 如果为 0，则语句未创建结果集;如果为 0，则语句未创建结果集。如果是任何其他数字，则语句确实创建了结果集。  
  
 在准备或执行语句后，应用程序可以随时调用**SQLNumResultCols。** 但是，由于某些数据源无法轻松描述由准备好的语句创建的结果集，因此，如果在准备语句后但在执行语句之前调用**SQLNumResultCols，** 性能将受到影响。  
  
 某些数据源还支持确定 SQL 语句在结果集中返回的行数。 为此，应用程序调用**SQLRowCount**。 行计数表示的确切内容由调用**SQLGetInfo**返回的SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2或SQL_STATIC_CURSOR_ATTRIBUTES2选项（取决于游标的类型）的设置指示。 此位掩码指示每个游标类型返回的行计数是精确、近似还是根本不可用。 静态或按键集驱动的游标的行计数是否受通过**SQLBulk操作**或**SQLSetPos**所做的更改或定位的更新或删除语句的影响，取决于前面列出的相同选项参数返回的其他位。 有关详细信息，请参阅[SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md)函数说明。
