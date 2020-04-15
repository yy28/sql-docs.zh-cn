---
title: Unicode |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9824e76cebabb6f5f84505292801a0094e359f0f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302440"
---
# <a name="unicode"></a>Unicode
Unicode 定义多种语言中的字符的编码。  
  
 有关 Unicode 标准的详细信息，请参阅[Unicode 联盟](https://www.unicode.org)。  
  
 Unicode 定义通用字符集。 Windows ANSI 代码页定义一个字符集，通常包含一种语言的字符。 编写需要使用不同的代码页的应用程序可能更加困难。  
  
 Unicode 不需要代码页。 每个代码点都映射到一种语言的单个字符。  
  
 目前，ODBC 支持的唯一 Unicode 编码是 UCS-2，它使用 16 位整数（固定长度）来表示字符。 Unicode 允许应用程序以不同的语言工作。  
  
 ODBC 3.5（或更高版本）驱动程序管理器启用了 Unicode。 这会影响两个主要区域：函数调用和字符串数据类型。 驱动程序管理器根据应用程序和驱动程序的要求映射函数字符串参数和字符串数据，这两个参数都可以启用 Unicode 或启用 ANSI。 这两个区域将在["Unicode 函数参数](../../../odbc/reference/develop-app/unicode-function-arguments.md)"和["Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)"部分中详细讨论。  
  
 ODBC 3.5（或更高版本）驱动程序管理器支持将 Unicode 驱动程序与 Unicode 应用程序和 ANSI 应用程序一起使用。 它还支持将 ANSI 驱动程序与 ANSI 应用程序一起使用。 驱动程序管理器为使用 ANSI 驱动程序的 Unicode 应用程序提供有限的 Unicode 到 ANSI 映射。  
  
 本部分包含以下主题。  
  
-   [Unicode 函数自变量](../../../odbc/reference/develop-app/unicode-function-arguments.md)  
  
-   [Unicode 数据](../../../odbc/reference/develop-app/unicode-data.md)
