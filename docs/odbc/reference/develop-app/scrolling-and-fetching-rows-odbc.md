---
title: 滚动和提取行 (ODBC) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 884c798e14964fbcaaf3ca9ba6656f4d62738fe8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62445973"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>滚动和提取行 (ODBC)
使用可滚动游标时，应用程序调用**SQLFetchScroll**来定位游标和提取行。 **SQLFetchScroll**支持相对滚动 (下一步，以前版本中，且相对*n*行)，绝对滚动 (first、 last、 和行*n*)，并按书签定位。 *FetchOrientation*并*FetchOffset*中的自变量**SQLFetchScroll**指定哪些行集提取，如以下关系图中所示。  
  
 ![接下来，提取之前，第一个和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **接下来，提取之前，第一个和最后一个行集**  
  
 ![提取绝对和相对的标有书签的行集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **提取绝对和相对的标有书签的行集**  
  
 **SQLFetchScroll**将游标定位到指定的行并在开头的行的行集返回的行。 如果指定的行集重叠结果集的末尾，则返回的部分行集。 如果指定的行集与重叠的结果的启动设置，在结果中的第一个行集通常返回集;有关完整详细信息，请参阅[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函数说明。  
  
 在某些情况下，应用程序可能想要将光标置于而没有检索任何数据。 例如，它可能会想要测试是否存在的行或只需获取该书签的行而不会降低跨网络的其他数据。 若要执行此操作，它设置为 SQL_RD_OFF SQL_ATTR_RETRIEVE_DATA 语句属性。 绑定到书签列 （如果有） 的变量始终会更新，而不考虑该语句属性的设置。  
  
 检索行集后，应用程序可以调用**SQLSetPos**要定位到行集中的行集或刷新行中的特定行。 有关使用的详细信息**SQLSetPos**，请参阅[使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  在 ODBC 2 支持滚动。*x*驱动程序通过**SQLExtendedFetch**。 有关详细信息，请参阅[块状游标、 可滚动游标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)中附录 g:为了向后兼容的驱动程序指南。
