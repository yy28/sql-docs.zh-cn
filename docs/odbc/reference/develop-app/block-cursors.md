---
title: 阻止游标 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 1a92b5d8-7c6e-4ce5-8c99-600a387026aa
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21bbfa223e2eb58df8fc89b69f7f9df3c08983e8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912152"
---
# <a name="block-cursors"></a>块状游标
许多应用程序花费大量时间将跨网络的数据。 这一次的一部分花费实际跨网络，使数据以及它的部分是在上所花费网络开销，例如，为请求的数据行所做的驱动程序调用。 如果应用程序能够高效地使用可以降低后一种时间*块，* 或*fat、* *光标、* 可一次返回多个行。  
  
 应用程序始终可以选择使用块状游标。 要从其提取一次只有一个行的数据源，必须驱动程序中模拟块状游标。 这可以通过执行多个单行更行提取。 虽然不太可能提供任何性能提升，这会打开应用程序的机会。 Dbms 本机实现块状游标以及与这些 Dbms 相关联的驱动程序将它们公开此类应用程序然后会提高性能。  
  
 与某个块游标读取一次返回的行被称为*行集*。 很重要不混淆随结果集的行集。 而行集维持应用程序缓冲区中，将在数据源中，保留结果集。 行集的结果集固定的而不是-它可以更改位置并内容每次提取一组新的行。 就像如当前行的传统 SQL 只进游标点单行游标，块状游标指向行集，可以被想象成*当前行*。  
  
 在已获取多个行时，请选择单个行上执行操作的操作，该应用程序必须首先指示哪些行是当前行。 当前行需要通过调用**SQLGetData**和定位 update 和 delete 语句。 当块状游标首先返回行集时，当前行是行集的第一个行。 若要更改的当前行中，应用程序调用**SQLSetPos**或**SQLBulkOperations** （若要更新书签）。 下图显示的结果集、 行集、 当前行、 行集游标，和块状游标的关系。 有关详细信息，请参阅[使用块状游标](../../../odbc/reference/develop-app/using-block-cursors.md)本部分中，将在后面和[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和[SQLSetPos 与更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
 ![接下来，提取之前，第一个和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 指示光标是否块状游标是否是可滚动无关。 例如，检索和打印行花费大部分报表应用程序中的工作。 因此，它将最快使用只进、 阻止光标。 它使用只进游标来避免可滚动游标和块状游标来减少网络流量的费用。  
  
 本部分包含以下主题。  
  
-   [绑定列用于块游标](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [行状态数组](../../../odbc/reference/develop-app/row-status-array.md)
