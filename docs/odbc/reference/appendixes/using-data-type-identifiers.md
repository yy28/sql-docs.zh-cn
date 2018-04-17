---
title: 使用数据类型标识符 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
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
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 283a4b6ed0fe2af5d29b619301f5a5dd283d22b5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="using-data-type-identifiers"></a>使用数据类型标识符
应用程序通过两种方式使用数据类型标识符： 描述其缓冲区到该驱动程序，以及如何检索有关的结果集从驱动程序，以便他们可以确定哪种类型的 C 将缓冲区中要用于存储数据的元数据。 应用程序调用以下函数以执行这些任务：  
  
-   **SQLBindParameter**， **SQLBindCol**，和**SQLGetData** -来描述应用程序缓冲区的 C 数据类型。  
  
-   **SQLBindParameter** -来描述的动态参数的 SQL 数据类型。  
  
-   **SQLColAttribute**和**SQLDescribeCol** -若要检索的结果集中的列的 SQL 数据类型。  
  
-   **SQLDescribeParameter** -检索 SQL 数据类型的参数。  
  
-   **SQLColumns**， **SQLProcedureColumns**，和**SQLSpecialColumns** -若要检索的各种架构信息的 SQL 数据类型  
  
-   **SQLGetTypeInfo** -若要检索的列表支持的数据类型  
  
 描述符的 SQL_DESC_CONCISE_TYPE 字段中存储数据类型的标识符。 描述符函数**SQLSetDescField**和**SQLSetDescRec**可以与相应的类型用于执行前面的列表中列出的任务。 有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
