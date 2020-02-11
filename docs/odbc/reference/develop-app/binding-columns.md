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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a634a553672b83931091056dd489f7559c4269b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106207"
---
# <a name="binding-columns"></a>绑定列
从数据源提取的数据将返回到应用程序已为此目的分配的变量中。 在完成此操作之前，应用程序必须将这些变量关联或*绑定*到结果集的列;从概念上讲，此过程与将应用程序变量绑定到语句参数相同。 当应用程序将变量绑定到结果集列时，它将描述该驱动程序的变量地址、数据类型等。 驱动程序将此信息存储在它为该语句维护的结构中，并在提取该行时使用该信息从列返回值。  
  
 本部分包含下列主题。  
  
-   [绑定结果集列](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [使用 SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md)
