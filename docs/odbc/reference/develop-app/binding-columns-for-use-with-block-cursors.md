---
title: 绑定列用于块游标 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0ed819643e7ea818fc17c0fa317473afc8f5ca3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63007862"
---
# <a name="binding-columns-for-use-with-block-cursors"></a>绑定列用于块游标
因为块状游标返回多个行，使用它们的应用程序必须将变量的数组绑定到每个列而不是单个变量。 这些列阵统称为*行集缓冲区*。 以下是绑定的两种样式:  
  
-   将数组绑定到每个列。 这称为*按列绑定*因为每个数据结构 （数组） 包含对单个列的数据。  
  
-   定义一种结构来保存整个行的数据，并将绑定这些结构的数组。 这称为*按行绑定*因为每个数据结构包含单个行的数据。  
  
 因为当应用程序将单个变量绑定到列，它将调用**SQLBindCol**要绑定到列的数组。 唯一的区别是传递的地址是数组地址，不要使用单个变量的地址。 应用程序设置 SQL_BIND_BY_COLUMN 语句属性指定是否使用按列绑定或按行绑定。 是否使用按列绑定或按行绑定很大程度的应用程序首选项。 按行绑定可能会更紧密地对应的数据的应用程序的布局，在这种情况下，它会提供更好的性能。  
  
 本部分包含以下主题。  
  
-   [按列绑定](../../../odbc/reference/develop-app/column-wise-binding.md)  
  
-   [按行绑定](../../../odbc/reference/develop-app/row-wise-binding.md)
