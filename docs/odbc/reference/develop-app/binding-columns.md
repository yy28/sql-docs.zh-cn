---
title: 绑定列 |Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301818"
---
# <a name="binding-columns"></a>绑定列
从数据源提取的数据将返回到应用程序已为此目的分配的变量中。 在完成此操作之前，应用程序必须将这些变量关联或*绑定*到结果集的列;从概念上讲，此过程与将应用程序变量绑定到语句参数相同。 当应用程序将变量绑定到结果集列时，它将描述该驱动程序的变量地址、数据类型等。 驱动程序将此信息存储在它为该语句维护的结构中，并在提取该行时使用该信息从列返回值。  
  
 本部分包含以下主题。  
  
-   [绑定结果集列](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
