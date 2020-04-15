---
title: 滚动和提取行 （ODBC） |微软文档
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
ms.openlocfilehash: 72d262bf73e69388f65ff281e62235d2d831669e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304198"
---
# <a name="scrolling-and-fetching-rows-odbc"></a>滚动和提取行 (ODBC)
使用可滚动游标时，应用程序调用**SQLFetchScroll**来定位游标并提取行。 **SQLFetchScroll**支持相对滚动（下一行、上行和相对*n*行）、绝对滚动（第一行、最后行和第*n*行）以及按书签进行定位。 **SQLFetchScroll**中的 *"提取方向*"和 *"提取偏移"* 参数指定要提取的行集，如下图所示。  
  
 ![提取下一个行集、上一个行集、第一个行集和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **提取下一个行集、上一个行集、第一个行集和最后一个行集**  
  
 ![提取绝对行集、相对行集和书签行集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **获取绝对、相对和书签的行集**  
  
 **SQLFetchScroll**将光标定位到指定的行，并返回行集中的行，从该行开始。 如果指定的行集与结果集的末尾重叠，则返回部分行集。 如果指定的行集与结果集的开始重叠，则通常返回结果集中的第一个行集;如果指定行集与结果集的开头重叠，则通常会返回结果集中的第一个行集。有关完整详细信息，请参阅[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函数说明。  
  
 在某些情况下，应用程序可能希望在不检索任何数据的情况下定位游标。 例如，它可能需要测试行是否存在，或者只是获取行的书签，而不通过网络传输其他数据。 为此，它将SQL_ATTR_RETRIEVE_DATA语句属性设置为SQL_RD_OFF。 绑定到书签列（如果有）的变量始终更新，而不考虑此属性的设置。  
  
 检索行集后，应用程序可以调用**SQLSetPos**定位到行集中的特定行或刷新行集中的行。 有关使用**SQLSetPos**的详细信息，请参阅[使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  ODBC 2 支持滚动。*x*驱动程序由**SQL 扩展获取**。 有关详细信息，请参阅附录 G 中的[块光标、可滚动光标和向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)：向后兼容性的驱动程序指南。
