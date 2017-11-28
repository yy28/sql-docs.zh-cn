---
title: "Unicode |Microsoft 文档"
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
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3e14c37b8246b3ffa541325f079b035424d2ff68
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="unicode"></a>Unicode
Unicode 定义许多语言中的字符编码。  
  
 有关 Unicode 标准的详细信息，请参阅[Unicode 协会](http://www.unicode.org)。  
  
 Unicode 定义通用的字符集。 Windows ANSI 代码页定义字符集，通常包含一种语言的字符。 它可能会更加难以编写的应用程序需要使用不同的代码页。  
  
 Unicode 不需要的代码页。 每个码位映射到某些语言中的单个字符。  
  
 目前，唯一的 Unicode 编码 ODBC 支持为 ucs-2、 使用 16 位整数 （固定长度） 来表示字符。 Unicode 允许应用程序中不同语言的工作。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器完全支持 Unicode。 这会影响两个主要区域： 函数调用和字符串数据类型。 驱动程序管理器映射函数字符串自变量和所需的应用程序和驱动程序的字符串数据，这两种可以是 Unicode 启用或 ANSI 已启用。 在部分中，详细地讨论了这两个方面[Unicode 函数自变量](../../../odbc/reference/develop-app/unicode-function-arguments.md)和[Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器支持使用 Unicode 应用程序和 ANSI 应用程序的 Unicode 驱动程序使用。 它还支持使用与 ANSI 应用程序的 ANSI 驱动程序。 驱动程序管理器提供了有限的 Unicode ANSI 映射为 Unicode 应用程序使用 ANSI 驱动程序。  
  
 本部分包含以下主题。  
  
-   [Unicode 函数自变量](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)
