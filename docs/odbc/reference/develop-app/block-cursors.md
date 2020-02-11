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
ms.openlocfilehash: 3e0ea6ff655140c979f400f67a59cd7259bac9e5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68118821"
---
# <a name="block-cursors"></a>块游标
许多应用程序花费大量时间将数据引入到网络中。 在这种情况下，实际上是在网络中使用数据，其中的部分数据消耗网络开销，例如由驱动程序发出的调用请求数据行。 如果应用程序有效使用*块*或*fat* *游标，* 则可以减少后一次使用，这些游标可以同时返回多行。  
  
 应用程序始终可以选择使用块游标。 对于每次只能提取一行的数据源，必须在驱动程序中模拟块游标。 可以通过执行多个单行读取来完成此操作。 虽然这不太可能提供任何性能提升，但它会为应用程序带来机会。 这样，此类应用程序就会经历性能提高，因为 Dbms 在本机实现了块游标，而与这些 Dbms 关联的驱动程序公开了这些游标  
  
 使用块游标在单个提取中返回的行称为*行集*。 不应将行集与结果集混淆，这一点很重要。 结果集在数据源中进行维护，而行集在应用程序缓冲区中维护。 如果结果集是固定的，则行集不会在每次提取新行集时更改位置和内容。 正如单行游标，如传统的 SQL 只进游标指向当前行，块游标指向行集，该行集可以被视为*当前行*。  
  
 若要在提取多个行时执行对单个行执行的操作，应用程序必须首先指示哪个行是当前行。 当前行是通过调用**SQLGetData**和定位的 update 和 delete 语句所必需的。 当块游标第一次返回行集时，当前行是行集的第一行。 若要更改当前行，应用程序将调用**SQLSetPos**或**SQLBulkOperations** （以便按书签进行更新）。 下图显示了结果集、行集、当前行、行集游标和块游标之间的关系。 有关详细信息，请参阅本部分后面的[使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)、[定位更新和删除语句](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md)和[使用 SQLSetPos 更新数据](../../../odbc/reference/develop-app/updating-data-with-sqlsetpos.md)。  
  
 ![提取下一个行集、上一个行集、第一个行集和最后一个行集](../../../odbc/reference/develop-app/media/pr20_2.gif "pr20_2")  
  
 游标是否为块游标与是否可滚动游标无关。 例如，报表应用程序中的大部分工作都用来检索和打印行。 因此，它将使用只进块游标最快。 它使用只进游标来避免滚动游标的开销，并使用块光标来减少网络流量。  
  
 本部分包含下列主题。  
  
-   [绑定列用于块游标](../../../odbc/reference/develop-app/binding-columns-for-use-with-block-cursors.md)  
  
-   [使用块游标](../../../odbc/reference/develop-app/using-block-cursors.md)  
  
-   [行状态数组](../../../odbc/reference/develop-app/row-status-array.md)
