---
title: "用于块状游标绑定列 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c527c2e89ab9acd0218a1b7f88112a81d537b780
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="binding-columns-for-use-with-block-cursors"></a>用于块状游标绑定列
由于块状游标返回多个行，使用它们的应用程序必须将数组变量绑定到每个列而不是单个变量。 这些阵列统称为*行集缓冲区*。 以下是绑定的两种样式:  
  
-   将数组绑定到每个列。 这称为*列绑定*因为每个数据结构 （数组） 包含单个列的数据。  
  
-   定义一种结构来容纳数据的整个行，并将绑定的这些结构数组。 这称为*按行绑定*因为每个数据结构包含单个行的数据。  
  
 因为当应用程序将单个变量绑定到列，它将调用**SQLBindCol**要绑定到列的数组。 唯一的区别是传递的地址是数组地址，非单个变量的地址。 应用程序将设置 SQL_BIND_BY_COLUMN 语句属性，用于指定是否使用按列或按行绑定。 是否使用按列或按行绑定很大程度的应用程序首选项。 按行绑定可能更紧密地对应的数据的应用程序的布局，在这种情况下，它将提供更好的性能。  
  
 本部分包含以下主题。  
  
-   [按列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)
