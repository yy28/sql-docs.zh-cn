---
title: Unicode |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC]
- Unicode [ODBC], about Unicode
ms.assetid: 113e1c9a-8333-4805-86f2-e4b57ab816a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a9ee58c367e83a61afef45d7df3358488dcb85a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47821065"
---
# <a name="unicode"></a>Unicode
Unicode 定义针对多种语言中的字符进行编码。  
  
 有关 Unicode 标准的详细信息，请参阅[Unicode Consortium](http://www.unicode.org)。  
  
 Unicode 定义通用字符集。 Windows ANSI 代码页定义字符集，通常包含一种语言的字符。 可能会更难编写的应用程序需要使用不同的代码页。  
  
 Unicode 不需要代码页。 每个代码点映射到某些语言中的单个字符。  
  
 目前，唯一的 Unicode 编码，ODBC 支持为 ucs-2，使用 16 位整数 （固定长度） 来表示字符。 Unicode 允许应用程序在不同的语言中工作。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器完全支持 Unicode。 这会影响两个主要领域： 函数调用，并且字符串数据类型。 驱动程序管理器映射函数的字符串参数和所需的应用程序和驱动程序的字符串数据，这两种可以是支持 Unicode 或 ANSI 已启用。 部分，详细讨论了这两个方面[Unicode 函数自变量](../../../odbc/reference/develop-app/unicode-function-arguments.md)并[Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)。  
  
 ODBC 3.5 （或更高版本） 驱动程序管理器支持 Unicode 驱动程序使用 Unicode 应用程序和 ANSI 应用程序的使用。 它还支持使用 ANSI 应用程序的 ANSI 驱动程序使用。 驱动程序管理器提供了有限的 Unicode 到 ANSI 映射为 Unicode 应用程序使用 ANSI 驱动程序。  
  
 本部分包含以下主题。  
  
-   [Unicode 函数自变量](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)
