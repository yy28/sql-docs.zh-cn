---
title: 滚动和提取行 (ODBC) |Microsoft 文档
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
- scrollable cursors [ODBC]
- fetches [ODBC], scrollable cursors
- cursors [ODBC], scrollable
- scrolling rows [ODBC]
ms.assetid: c43764cb-5841-4b89-9dc0-984a7488b3c1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 273046a04849b0b1501e2dd4be476c9abb540c5f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="scrolling-and-fetching-rows-odbc"></a>滚动和提取行 (ODBC)
使用可滚动游标时，应用程序调用**SQLFetchScroll**定位游标和提取行。 **SQLFetchScroll**支持相对滚动 (下一步、 之前，和相对*n*行)，绝对滚动 (名字、 姓氏，和行*n*)，和由书签定位。 *FetchOrientation*和*FetchOffset*中的自变量**SQLFetchScroll**指定要提取，哪些行集，如以下关系图中所示。  
  
 ![接下来，提取之前，第一个和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 **接下来，提取之前，第一个和最后一个行集**  
  
 ![提取绝对、 相对和书签的行集](../../../odbc/reference/develop-app/media/pr20_1.gif "pr20_1")  
  
 **提取绝对、 相对和书签的行集**  
  
 **SQLFetchScroll**定位光标所在位置到指定的行并在开头该行的行集返回的行。 如果指定的行集重叠结果集的末尾，则返回的部分行集。 如果指定的行集重叠的结果的开始设置，在结果中的第一个行集通常返回集;有关完整详细信息，请参阅[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)函数说明。  
  
 在某些情况下，应用程序可能想要将光标的位置而不检索任何数据。 例如，它可能想要测试是否存在行或者只获取书签的行不跨网络将其他数据的情况下。 若要执行此操作，它设置为 SQL_RD_OFF SQL_ATTR_RETRIEVE_DATA 语句属性。 变量绑定到书签列 （如果有） 会始终更新，而不考虑此语句属性的设置。  
  
 在检索行集后，应用程序可以调用**SQLSetPos**要定位到行集中的行集或刷新行中的特定行。 有关详细信息使用**SQLSetPos**，请参阅[更新数据与 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
> [!NOTE]  
>  滚动 ODBC 2 支持。*x*驱动程序通过**SQLExtendedFetch**。 有关详细信息，请参阅[块状游标可滚动游标，向后兼容性](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md)为了向后兼容的附录 g： 驱动程序准则中。
