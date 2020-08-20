---
description: 目录数据的用法
title: 目录数据的使用 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog data [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], using catalog data
ms.assetid: d5915d0c-eec3-4382-850e-bd863763c99a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7e03dff0a8c5715a86f1bcdff65b74f55409889a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471194"
---
# <a name="uses-of-catalog-data"></a>目录数据的用法
应用程序以各种方式使用目录数据。 下面是一些常见用途：  
  
-   **在运行时构造 SQL 语句。** 垂直应用程序（如订单输入应用程序）包含硬编码的 SQL 语句。 应用程序使用的表和列提前固定，这与访问这些表的语句是一样的。 例如，订单输入应用程序通常包含一个参数化 **INSERT** 语句，用于向系统添加新订单。  
  
     一般应用程序（如使用 ODBC 检索数据的电子表格程序）通常在运行时基于用户输入构造 SQL 语句。 此类应用程序可能要求用户键入要使用的表和列的名称。 但是，如果应用程序显示的表和列的列表与用户可从中进行选择的表和列的列表，则用户会更容易。 若要生成这些列表，应用程序将调用 **SQLTables** 和 **SQLColumns** 目录函数。  
  
-   **在开发过程中构造 SQL 语句。** 应用程序开发环境通常允许编程人员在开发程序时创建数据库查询。 然后在生成的应用程序中对查询进行硬编码。  
  
     此类环境还可以使用 **SQLTables** 和 **SQLColumns** 来创建程序员可从中进行选择的列表。 这些环境还可以使用 **SQLPrimaryKeys** 和 **SQLForeignKeys** 来自动确定和显示所选表之间的关系，并使用 **SQLStatistics** 来确定和突出显示索引字段，以便程序员可以创建高效的查询。  
  
-   **构造游标。** 提供可滚动的游标引擎的应用程序、驱动程序或中间件可以使用 **SQLSpecialColumns** 来确定唯一标识行的一列或多列。 该程序可以为已提取的每行生成一个包含这些列的值的 *键集* 。 当应用程序向后滚动到行时，它将使用这些值来提取行的最新数据。 有关可滚动游标和键集的详细信息，请参阅可 [滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。
