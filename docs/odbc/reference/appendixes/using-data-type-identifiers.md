---
title: 使用数据类型标识符 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f14294b76fc7977de256697c730f7dca31e7a469
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735125"
---
# <a name="using-data-type-identifiers"></a>使用数据类型标识符
应用程序通过两种方式使用数据类型标识符： 来描述其缓冲区指向该驱动程序，并检索有关结果集从驱动程序，以便他们可以确定哪种类型的 C 缓冲要用于存储数据的元数据。 应用程序调用以下函数来执行这些任务：  
  
-   **SQLBindParameter**， **SQLBindCol**，和**SQLGetData** -来描述应用程序缓冲区的 C 数据类型。  
  
-   **SQLBindParameter** -来描述的动态参数的 SQL 数据类型。  
  
-   **SQLColAttribute**并**SQLDescribeCol** -检索结果集列的 SQL 数据类型。  
  
-   **SQLDescribeParameter** -检索 SQL 数据类型的参数。  
  
-   **SQLColumns**， **SQLProcedureColumns**，和**SQLSpecialColumns** -检索 SQL 数据类型的各种架构信息  
  
-   **SQLGetTypeInfo** -检索受支持的数据类型的列表  
  
 数据类型标识符存储在描述符的 SQL_DESC_CONCISE_TYPE 字段中。 描述符函数**SQLSetDescField**并**SQLSetDescRec**可以在适当的类型来执行前面的列表中列出的任务。 有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
