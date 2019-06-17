---
title: 目录数据的用法 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d9b75d59d8fc28e364f5826d95e7fc50cb6afda7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63312524"
---
# <a name="uses-of-catalog-data"></a>目录数据的用法
应用程序使用不同的方式中的目录数据。 下面是一些常见用途：  
  
-   **在运行时构造 SQL 语句。** 垂直应用程序，如订单输入应用程序，包含硬编码的 SQL 语句。 表和应用程序使用的列被固定的提前，以及访问这些表的语句。 例如，订单输入应用程序通常包含单个参数化**插入**向系统添加新订单的语句。  
  
     泛型应用程序，如电子表格程序使用 ODBC 检索数据，通常在运行时根据用户输入构造 SQL 语句。 此类应用程序可能要求用户键入的表和要使用的列的名称。 但是，将会更容易为用户如果应用程序显示的表和用户可以从中进行选择的列的列表。 若要生成这些列表，该应用程序应该调用**SQLTables**并**SQLColumns**目录函数。  
  
-   **在开发过程中构造 SQL 语句。** 通常情况下，应用程序开发环境允许程序员要开发某个程序的同时创建数据库查询。 然后，查询是构建应用程序中硬编码。  
  
     也可以使用此类环境**SQLTables**并**SQLColumns**创建程序员可以从中进行选择的列表。 此外可以使用这些环境**SQLPrimaryKeys**并**SQLForeignKeys**自动确定并显示所选表之间的关系并使用**SQLStatistics**来确定并突出显示索引的字段，因此程序员可以创建高效的查询。  
  
-   **构造的游标。** 可以使用应用程序、 驱动程序或提供可滚动游标引擎的中间件**SQLSpecialColumns**来确定哪些列或多列唯一标识行。 该程序可以构建*由键集*包含这些行的列的每个已提取的值。 当应用程序滚动回行时，它然后将使用这些值来提取行的最新数据。 有关可滚动游标和键集的详细信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。
