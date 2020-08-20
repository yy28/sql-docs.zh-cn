---
description: 滚动和提取行 (ODBC)
title: " (ODBC) 滚动和提取行 |Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6fcdd2cd635a7da66a5d81c4beb24088f96382b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476489"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>滚动和提取行 (ODBC)
使用可滚动游标时，应用程序调用 **SQLFetchScroll** 来定位游标并提取行。 **SQLFetchScroll** 支持相对滚动 (next、前期和相对 *n* 行) ，绝对滚动 (first、last 和 row *n*) ，并按书签定位。 **SQLFetchScroll**中的*FetchOrientation*和*FetchOffset*参数指定要提取的行集，如下图所示。  
  
 ![提取下一个行集、上一个行集、第一个行集和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **提取下一个行集、上一个行集、第一个行集和最后一个行集**  
  
 ![提取绝对行集、相对行集和书签行集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **提取绝对、相对和书签的行集**  
  
 **SQLFetchScroll** 将游标定位到指定的行，并以该行开头返回行集中的行。 如果指定的行集与结果集的末尾重叠，则返回部分行集。 如果指定的行集与结果集的开头重叠，则通常返回结果集中的第一个行集;有关完整的详细信息，请参阅 [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) 函数说明。  
  
 在某些情况下，应用程序可能需要在不检索任何数据的情况下定位游标。 例如，它可能需要测试行是否存在，或者只是获取行的书签，而不会在网络中引入其他数据。 为此，它会将 SQL_ATTR_RETRIEVE_DATA 语句特性设置为 SQL_RD_OFF。 如果始终更新任何) ，则绑定到 bookmark 列的变量 (，而不考虑此语句特性的设置。  
  
 检索到行集之后，应用程序可以调用 **SQLSetPos** ，以便定位到行集中的特定行或刷新行集中的行。 有关使用 **SQLSetPos**的详细信息，请参阅 [使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  ODBC 2 支持滚动。*x* 驱动程序 **SQLExtendedFetch**。 有关详细信息，请参阅附录 G：驱动程序准则中的 [块游标、可滚动游标和后向兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)。
