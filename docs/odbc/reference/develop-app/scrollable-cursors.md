---
title: 可滚动游标 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: 2c8a5f50-9b37-452f-8160-05f42bc4d97e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2762ffc7fa179fc6a68f92c23f92ca12803f5ab7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304208"
---
# <a name="scrollable-cursors"></a>可滚动游标
在基于新式屏幕的应用程序中，用户向后滚动数据。 对于此类应用程序，返回之前提取的行是一个问题。 一种可能的做法是先关闭再重新打开游标，然后提取行，直到光标到达所需的行。 另一种可能的方法是读取结果集，将其缓存在本地，并在应用程序中实现滚动。 这两种可能性仅适用于较小的结果集，而后一种可能性很难实现。 更好的解决方案是使用可*滚动的游标，该游标*可以在结果集中向后和向前移动。  
  
 可*滚动的游标*通常用于基于新式屏幕的应用程序中，用户可以在这些应用程序中来回滚动数据。 但是，仅当只进游标不执行此作业时，应用程序才应使用可滚动游标，因为可滚动游标的开销通常比只进游标更昂贵。  
  
 向后移动的功能引发了不适用于只进游标的问题：可滚动的游标是否检测对以前提取的行所做的更改？ 也就是说，是否应检测更新、删除和新插入的行？  
  
 出现这一问题的原因在于，结果集的定义（一组符合特定条件的行）在检查行是否与该条件匹配时不会出现问题，也不指出每次提取行时是否必须包含相同的数据。 以前的省略使可滚动游标能够检测行是否已插入或删除，而后者则可以使它们检测更新的数据。  
  
 检测更改的功能有时很有用。 例如，会计应用程序需要一个忽略所有更改的游标;如果光标显示最新更改，则无法平衡书籍。 另一方面，航空公司预订系统需要一个显示数据的最新更改的光标;如果没有此类游标，它必须不断地重新查询数据库以显示最新的航班可用性。  
  
 为了满足不同应用程序的需求，ODBC 定义了四种不同类型的可滚动游标。 这些游标的支出和检测结果集更改的能力会有所不同。 请注意，如果可滚动游标可以检测对行所做的更改，则在尝试重新提取这些行时，它只能检测它们;数据源无法向游标通知当前提取行的更改。 请注意，更改的可见性也由事务隔离级别控制;有关详细信息，请参阅[事务隔离](../../../odbc/reference/develop-app/transaction-isolation.md)。  
  
 本部分包含以下主题。  
  
-   [可滚动游标类型](../../../odbc/reference/develop-app/scrollable-cursor-types.md)  
  
-   [使用可滚动游标](../../../odbc/reference/develop-app/using-scrollable-cursors.md)  
  
-   [相对和绝对滚动](../../../odbc/reference/develop-app/relative-and-absolute-scrolling.md)  
  
-   [书签](../../../odbc/reference/develop-app/bookmarks-odbc.md)
