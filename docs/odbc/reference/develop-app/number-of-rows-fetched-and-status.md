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
ms.openlocfilehash: bc1f556873221faa3f86c5272120a786f6f25025
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086332"
---
# <a name="number-of-rows-fetched-and-status"></a>提取的行数和状态
如果已设置 SQL_ATTR_ROWS_FETCHED_PTR 语句特性，则它指定一个缓冲区，该缓冲区返回通过调用**SQLFetch**或**SQLFetchScroll**以及错误行提取的行数。 （此数字是不具有状态 SQL_ROW_NO_ROWS 的所有行的计数。）调用**SQLBulkOperations**或**SQLSetPos**后，该缓冲区包含受该函数执行的大容量操作影响的行数。 如果已设置 SQL_ATTR_ROW_STATUS_PTR 语句特性，则**SQLFetch**或**SQLFetchScroll**将返回*行状态数组，该行状态数组*提供每个返回行的状态。 这些字段指向的两个缓冲区由应用程序分配并由驱动程序填充。 在关闭游标之前，应用程序必须确保这些指针保持有效。  
  
 行状态数组中的条目指出是否已成功提取每行，是否在上次提取行后对其进行更新、添加或删除，以及在提取行时是否出错。 如果**SQLFetch**或**SQLFetchScroll**在检索多行行集中的一行时遇到错误，或者如果**SQLBulkOperations**的*操作*SQL_FETCH_BY_BOOKMARK 参数在执行批量提取时遇到错误，则会将行状态数组中的相应值设置为 SQL_ROW_ERROR，继续提取行并返回 SQL_SUCCESS_WITH_INFO。 有关错误处理和行状态数组的详细信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)和[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函数说明。
