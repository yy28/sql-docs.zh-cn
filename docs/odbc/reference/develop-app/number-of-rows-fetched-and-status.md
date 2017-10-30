---
title: "提取的行数和状态 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3e79fec9836fb7a6528bea63c78a8e6479dac8e1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="number-of-rows-fetched-and-status"></a>提取的行数和状态
如果已经设置了 SQL_ATTR_ROWS_FETCHED_PTR 语句特性，它指定返回通过调用提取的行数的缓冲区**SQLFetch**或**SQLFetchScroll**，和错误行。 （此数字是没有状态 SQL_ROW_NO_ROWS 的所有行的计数。）调用了**SQLBulkOperations**或**SQLSetPos**，该缓冲区包含受函数中执行的大容量操作的行数。 如果已经设置了 SQL_ATTR_ROW_STATUS_PTR 语句特性， **SQLFetch**或**SQLFetchScroll**返回*行状态数组*该属性提供的每个状态返回的行。 这两个指向这些字段的缓冲区分配由应用程序和驱动程序填充。 应用程序必须确保这些指针保持有效，直到关闭光标。  
  
 行状态数组状态中的条目是否已更新，是否成功，提取每个行添加，或者删除由于上次提取，以及是否可以提取行时出错。 如果**SQLFetch**或**SQLFetchScroll**时遇到错误时检索一行的多行的行集，或者如果**SQLBulkOperations**与*操作* SQL_FETCH_BY_BOOKMARK 自变量执行大容量提取时遇到错误，它设置到 SQL_ROW_ERROR 的行状态数组中的相应值，将继续提取行，并返回 SQL_SUCCESS_WITH_INFO。 有关错误处理和行状态数组的详细信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)和[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函数说明。

