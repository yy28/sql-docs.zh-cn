---
title: 目录数据的使用 |微软文档
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
ms.openlocfilehash: 429d42d4a82d0f9f34e33eb4f5f3293100505da9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306808"
---
# <a name="uses-of-catalog-data"></a>目录数据的用法
应用程序以各种方式使用目录数据。 下面是一些常见的用途：  
  
-   **在运行时构造 SQL 语句。** 垂直应用程序（如订单输入应用程序）包含硬编码的 SQL 语句。 应用程序使用的表和列提前修复，访问这些表的语句也提前修复。 例如，订单输入应用程序通常包含单个参数化**的 INSERT**语句，用于向系统添加新订单。  
  
     通用应用程序（如使用 ODBC 检索数据的电子表格程序）通常根据用户输入在运行时构造 SQL 语句。 此类应用程序可能要求用户键入要使用的表和列的名称。 但是，如果应用程序显示用户可以从中进行选择的表和列的列表，则用户会更容易。 要生成这些列表，应用程序将调用**SQLTables**和**SQLColumns**目录函数。  
  
-   **在开发过程中构造 SQL 语句。** 应用程序开发环境通常允许程序员在开发程序时创建数据库查询。 然后，在正在生成的应用程序中对查询进行硬编码。  
  
     此类环境还可以使用**SQLTables**和**SQLColumns**创建程序员可以从中进行选择的列表。 这些环境还可能使用**SQLPrimaryKeys**和**SQL 外键**自动确定和显示所选表之间的关系，并使用**SQLStatistics**来确定和突出显示索引字段，以便程序员可以创建高效的查询。  
  
-   **构造游标。** 提供可滚动游标引擎的应用程序、驱动程序或中间件可以使用**SQL 特别列**来确定哪个列或列唯一标识一行。 程序可以生成一个*键集*，其中包含已提取的每行的这些列的值。 当应用程序滚动回行时，它将使用这些值获取该行的最新数据。 有关可滚动游标和键集的详细信息，请参阅[可滚动游标](../../../odbc/reference/develop-app/scrollable-cursors.md)。
