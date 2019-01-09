---
title: 块游标 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc62e7b5225c434bac33630f2f0cf8f39c72bfc9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52504679"
---
# <a name="block-cursors"></a>块游标
许多应用程序花费大量的时间将跨网络的数据。 这次所用的部分实际上将数据传送跨网络，以及作为其中一部分所用的网络开销，如驱动程序请求数据的行所做的调用。 如果应用程序可以有效地使用后一种时间就会降低*块中，* 或*fat* *游标，* 这可以一次返回多个行。  
  
 应用程序始终能够使用块状游标的选项。 要从其提取一次只有一个行的数据源，必须在驱动程序中模拟块状游标。 这可以通过执行多个单行提取操作。 虽然不太可能提供任何性能提升，它会打开应用程序的机会。 此类应用程序然后将使性能提高，如 Dbms 本机实现块状游标并关联与这些 Dbms 的驱动程序公开它们。  
  
 使用块游标读取一次返回的行被称为*行集*。 务必不要将混淆的结果集与行集。 而在行集中维护应用程序缓冲区中，结果集保留在数据源。 结果集固定的而未将行集-更改位置并且内容每次提取一组新的行。 如对当前行的传统 SQL 只进游标点单行游标，就像块状游标指向行集，可以将看作*当前行*。  
  
 若要执行操作的操作的单个行，已提取的多个行时，应用程序必须首先指示哪些行是当前行。 当前行通过调用所需**SQLGetData**和定位 update 和 delete 语句。 当块游标首先返回行集时，当前行是行集的第一个行。 若要更改的当前行中，应用程序调用**SQLSetPos**或**SQLBulkOperations** （为了按书签更新）。 下图显示了结果集、 行集、 当前行、 行集游标和块状游标的关系。 有关详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)本部分中，将在后面和[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)并[使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
 ![接下来，提取之前，第一个和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 指示光标是否块状游标不依赖于它是否可滚动。 例如，检索和打印的行所用的大部分报表应用程序中工作。 因此，它将最快使用只进、 阻止游标。 它使用只进游标来避免可滚动游标和块状游标来减少网络流量的费用。  
  
 本部分包含以下主题。  
  
-   [绑定列用于块游标](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [行状态数组](../../../odbc/reference/develop-app/row-status-array.md)
