---
title: 使用数据类型标识符 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8be8eef0441d48ed03ea6ccf8f656627c1dd9b63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301418"
---
# <a name="using-data-type-identifiers"></a>使用数据类型标识符
应用程序使用数据类型标识符的方式有两种：向驱动程序描述其缓冲区，以及从驱动程序检索有关结果集的元数据，以便确定用于存储数据的 C 缓冲区类型。 应用程序调用以下函数来执行这些任务：  
  
-   **SQLBind参数****、SQLBindCol**和**SQLGetData** - 描述应用程序缓冲区的 C 数据类型。  
  
-   **SQLBind参数**- 描述动态参数的 SQL 数据类型。  
  
-   **SQLColAttribute**和**SQLDescribeCol** - 检索结果集列的 SQL 数据类型。  
  
-   **SQL描述参数**- 检索参数的 SQL 数据类型。  
  
-   **SQL列****、SQL程序列**和**SQL 特殊列**- 检索各种架构信息的 SQL 数据类型  
  
-   **SQLGetTypeInfo** - 检索受支持的数据类型列表  
  
 数据类型标识符存储在描述符的SQL_DESC_CONCISE_TYPE字段中。 描述符功能**SQLSetDescField**和**SQLSetDescCRec**可与适当的类型一起使用，以执行上一列表中列出的任务。 有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
