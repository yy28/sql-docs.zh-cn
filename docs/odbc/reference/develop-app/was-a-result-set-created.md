---
description: 是否创建了一个结果集？
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
ms.openlocfilehash: 57b65c254f48d9c3f5078c3b2c1f576ae54d4740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421381"
---
# <a name="was-a-result-set-created"></a>是否创建了一个结果集？
在大多数情况下，应用程序程序员知道其应用程序执行的语句是否会创建结果集。 如果应用程序使用程序员编写的硬编码 SQL 语句，就会出现这种情况。 当应用程序在运行时构造 SQL 语句时，通常是这样的：程序员可以轻松地包含标记是否正在构造 **SELECT** 语句或 **INSERT** 语句的代码。 在少数情况下，程序员不可能知道语句是否会创建结果集。 如果应用程序提供了一种方法来输入和执行 SQL 语句，则此值为 true。 当应用程序在运行时构造语句来执行过程时也是如此。  
  
 在这种情况下，应用程序会调用 **SQLNumResultCols** 来确定结果集中的列数。 如果此值为0，则语句未创建结果集;如果此值为其他任何数字，则该语句将创建结果集。  
  
 在准备或执行语句后，应用程序可以随时调用 **SQLNumResultCols** 。 但是，因为某些数据源不能轻松地描述将由预定义的语句创建的结果集，所以如果在准备语句之后但在执行语句之前调用 **SQLNumResultCols** ，则性能将会降低。  
  
 某些数据源还支持确定 SQL 语句在结果集中返回的行数。 为此，应用程序将调用 **SQLRowCount**。 行计数所代表的确切内容由 SQL_DYNAMIC_CURSOR_ATTRIBUTES2、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES2、SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 选项的设置指示 (具体取决于通过调用 **SQLGetInfo**返回的游标的类型。 此位掩码指示每个游标类型是返回的行计数是精确、近似还是根本不可用。 静态或由键集驱动的游标的行计数是否受通过 **SQLBulkOperations** 或 **SQLSetPos**所做的更改和定位的 update 或 delete 语句的影响，取决于前面列出的相同选项参数返回的其他位。 有关详细信息，请参阅 [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) 函数说明。
