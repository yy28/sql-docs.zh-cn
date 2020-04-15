---
title: 绑定列 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fca4cfb1455c91ca57f7b1769266e2040d6a3511
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301818"
---
# <a name="binding-columns"></a>绑定列
从数据源获取的数据以应用程序为此分配的变量返回到应用程序。 在此操作之前，应用程序必须将这些变量关联或绑定到结果集的列;否则，应用程序必须将这些变量关联或*绑定*到结果集的列中。从概念上讲，此过程与绑定应用程序变量到语句参数相同。 当应用程序将变量绑定到结果集列时，它将该变量 （地址、数据类型等） 描述给驱动程序。 驱动程序将此信息存储在它为该语句维护的结构中，并使用该信息在提取行时从列返回值。  
  
 本部分包含以下主题。  
  
-   [绑定结果集列](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
