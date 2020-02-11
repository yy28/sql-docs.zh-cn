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
ms.openlocfilehash: 2b5e9fea64986bf595676540d74bb87a6e62521c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68070009"
---
# <a name="using-data-type-identifiers"></a>使用数据类型标识符
应用程序通过两种方式使用数据类型标识符：向驱动程序描述其缓冲区，并从驱动程序检索有关结果集的元数据，以便它们能够确定要用于存储数据的 C 缓冲区类型。 应用程序调用以下函数来执行这些任务：  
  
-   **SQLBindParameter**、 **SQLBindCol**和**SQLGetData** -描述应用程序缓冲区的 C 数据类型。  
  
-   **SQLBindParameter** -描述动态参数的 SQL 数据类型。  
  
-   **SQLColAttribute**和**SQLDescribeCol** -检索结果集列的 SQL 数据类型。  
  
-   **SQLDescribeParameter** -检索参数的 SQL 数据类型。  
  
-   **SQLColumns**、 **SQLProcedureColumns**和**SQLSpecialColumns** -检索各种架构信息的 SQL 数据类型  
  
-   **SQLGetTypeInfo** -检索支持的数据类型的列表  
  
 数据类型标识符存储在描述符的 SQL_DESC_CONCISE_TYPE 字段中。 描述符函数**SQLSetDescField**和**SQLSetDescRec**可用于适当的类型，以执行上列表中列出的任务。 有关详细信息，请参阅[SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)。
