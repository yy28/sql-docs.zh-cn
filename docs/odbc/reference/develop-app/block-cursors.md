---
title: 块光标 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa35888ef93da9648fe6422bdc35ebf9da3a0525
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306348"
---
# <a name="block-cursors"></a>块游标
许多应用程序花费大量时间通过网络传输数据。 这一时间的一部分实际上用于将数据带入整个网络，其中一部分用于网络开销，例如驱动程序调用请求一行数据。 如果应用程序有效地使用块或*胖**光标，* 则可以减少后一时间，因为*块*或胖光标一次可以返回多个行。  
  
 应用程序始终可以选择使用块游标。 在一次只能提取一行的数据源上，必须在驱动程序中模拟块游标。 这可以通过执行多个单行提取来实现。 虽然这不太可能带来任何性能提升，但它为应用程序提供了机会。 然后，随着 DBMS 本机实现块游标以及与这些 DBMS 关联的驱动程序公开它们，此类应用程序的性能将提升。  
  
 在具有块游标的单个提取中返回的行称为*行集*。 重要的是不要将行集与结果集混淆。 结果集保存在数据源中，而行集则保存在应用程序缓冲区中。 当结果集是固定的时，行集不是 - 每次提取一组新的行时，都会更改位置和内容。 正如单行游标（如传统的 SQL 仅向前游标）指向当前行一样，块游标指向行集，这可视为*当前行*。  
  
 要在提取多行时对一行执行操作，应用程序必须首先指示哪行是当前行。 调用**SQLGetData**和定位更新和删除语句需要当前行。 当块游标首次返回行集时，当前行是行集的第一行。 要更改当前行，应用程序将调用**SQLSetPos**或**SQLBulk 操作**（按书签更新）。 下图显示了结果集、行集、当前行、行集游标和块游标的关系。 有关详细信息，请参阅在本部分后面的[中使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)，以及[使用 SQLSetPos](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和更新数据。  
  
 ![提取下一个行集、上一个行集、第一个行集和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 游标是否是块游标，与游标是否可滚动无关。 例如，报表应用程序中的大部分工作都用于检索和打印行。 因此，它将以最快速度使用仅转发块游标。 它使用仅转发游标来避免可滚动游标的费用，使用块游标来减少网络流量。  
  
 本部分包含以下主题。  
  
-   [绑定列用于块游标](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [行状态数组](../../../odbc/reference/develop-app/row-status-array.md)
