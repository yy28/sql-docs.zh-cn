---
title: 已提取的行数和状态 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20e1632e8da765b0da2785bd846b67d13ebe01ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302358"
---
# <a name="number-of-rows-fetched-and-status"></a>提取的行数和状态
如果已设置SQL_ATTR_ROWS_FETCHED_PTR语句属性，它将指定一个缓冲区，该缓冲区返回调用**SQLFetch**或**SQLFetchScroll**获取的行数，以及错误行。 （此数字是未SQL_ROW_NO_ROWS状态的所有行的计数。调用**SQLBulk 操作**或**SQLSetPos**后，缓冲区包含受函数执行的批量操作影响的行数。 如果设置了SQL_ATTR_ROW_STATUS_PTR语句属性 **，SQLFetch**或**SQLFetchScroll**将返回*行状态数组，该数组*提供每个返回行的状态。 这些字段指向的两个缓冲区都由应用程序分配并由驱动程序填充。 应用程序必须确保这些指针保持有效，直到光标关闭。  
  
 行状态数组中的条目状态每行是否成功提取，自上次提取行以来是否更新、添加或删除，以及获取行时是否发生错误。 如果**SQLFetch**或**SQLScroll**在检索多行行集的一行时遇到错误，或者如果具有*操作*参数的**SQLBulk 操作**SQL_FETCH_BY_BOOKMARK在执行批量提取时遇到错误，则它将行状态数组中的相应值设置为SQL_ROW_ERROR，继续提取行，并返回SQL_SUCCESS_WITH_INFO。 有关错误处理和行状态数组的详细信息，请参阅[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)和[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函数说明。
