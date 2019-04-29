---
title: 提取的行数和状态 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- number of rows fetched [ODBC]
- result sets [ODBC], row status array
ms.assetid: a069b979-5108-4905-932f-8ae8e7905ff2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ab4830ddd56335959dd7049a1dabdcc3a0354213
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63149333"
---
# <a name="number-of-rows-fetched-and-status"></a>提取的行数和状态
如果将 SQL_ATTR_ROWS_FETCHED_PTR 语句属性尚未设置，它指定返回通过调用提取的行数的缓冲区**SQLFetch**或**SQLFetchScroll**，和错误行。 （此数字是没有状态 SQL_ROW_NO_ROWS 的所有行的计数。）在调用**SQLBulkOperations**或**SQLSetPos**，该缓冲区包含受影响的函数中执行的大容量操作的行数。 如果已设置 SQL_ATTR_ROW_STATUS_PTR 语句属性， **SQLFetch**或**SQLFetchScroll**返回*行状态数组*提供每个状态返回的行。 这两个由这些字段指向的缓冲区分配应用程序和驱动程序填充。 应用程序必须确保这些指针保持有效，直到关闭游标。  
  
 行状态数组状态中的条目是否已更新，成功，提取每个行添加，还是删除由于上次提取，以及是否可以提取行时出错。 如果**SQLFetch**或**SQLFetchScroll**检索多行的行集的一行时遇到错误或者，如果**SQLBulkOperations**与*操作* SQL_FETCH_BY_BOOKMARK 的自变量执行大容量提取时遇到错误，它设置到 SQL_ROW_ERROR 的行状态数组中的相应值，将继续提取行，并返回 SQL_SUCCESS_WITH_INFO。 有关错误处理和行状态数组的详细信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)并[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函数说明。
