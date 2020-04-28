---
title: 用于块游标的绑定列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column-wise binding [ODBC]
- row-wise binding [ODBC]
- result sets [ODBC], binding columns
- cursors [ODBC], block
- binding columns [ODBC]
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 231beede-cdfa-4e28-8b10-2760b983250f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc7e527658a7d6945921510de898c648075c41fc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284897"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>绑定列用于块游标
由于块游标返回多行，因此使用它们的应用程序必须将变量数组绑定到每个列而不是一个变量。 这些数组统称为*行集缓冲区*。 下面是两种绑定样式：  
  
-   将数组绑定到每个列。 这称为按*列绑定*，因为每个数据结构（数组）都包含单个列的数据。  
  
-   定义一个结构来保存整行的数据，并绑定这些结构的数组。 这称为按*行绑定*，因为每个数据结构包含单个行的数据。  
  
 当应用程序将单个变量绑定到列时，它将调用**SQLBindCol**将数组绑定到列。 唯一的区别在于传递的地址是数组地址，而不是单个变量地址。 应用程序设置 SQL_BIND_BY_COLUMN 语句特性来指定它是使用按列绑定还是按行绑定。 是使用按列绑定还是按行绑定，在很大程度上取决于应用程序首选项。 按行绑定可能更接近应用程序的数据布局，在这种情况下，它可以提供更好的性能。  
  
 本部分包含以下主题。  
  
-   [按列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)
