---
title: "绑定列 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 072ca1b754159efbd117f4530f458caf8fb40c0d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="binding-columns"></a>绑定列
从数据源提取的数据返回到应用程序已为此目的分配的变量中的应用程序中。 进行这种之前，必须将应用程序进行关联，或*绑定*，设置到结果的列的这些变量; 从概念上讲，此过程与将应用程序变量绑定到语句参数相同。 当应用程序将绑定到变量的结果集列，它描述了该变量-地址、 数据类型和等等 — 于驱动程序。 该驱动程序将此信息存储在它维护适用于该语句，并使用的信息来从列返回的值，当读取行的结构。  
  
 本部分包含以下主题。  
  
-   [绑定结果集列](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
