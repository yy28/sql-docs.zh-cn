---
title: 翻译 Dll |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3dad12bcd71434c1013b4fde5b4bd0231e56016f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81297942"
---
# <a name="translation-dlls"></a>转换 DLL
应用程序和数据源通常将数据存储在不同的字符集中。 ODBC 提供了一种通用机制，使驱动程序可以将数据从一个字符集转换到另一个字符集。 它包含实现转换函数**SQLDriverToDataSource**和**SQLDataSourceToDriver**的 DLL，驱动程序调用该函数来转换数据源和驱动程序之间流动的所有数据。 此 DLL 可由应用程序开发人员、驱动程序开发人员或第三方编写。  
  
 可以在该数据源的系统信息中指定特定数据源的转换 DLL;有关详细信息，请参阅[数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)。 还可以在运行时设置它，并在 SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION 连接属性。  
  
 转换选项是只能由特定翻译 DLL 解释的值。 例如，如果翻译 DLL 在不同的代码页之间转换，则选项可能会提供应用程序和数据源所使用的代码页的数目。 翻译 DLL 不需要使用转换选项。  
  
 指定翻译 DLL 之后，驱动程序将加载它并调用它来转换应用程序和数据源之间流动的所有数据。 这包括发送到数据源的所有 SQL 语句和字符参数，以及所有字符结果、字符元数据（如列名称）以及从数据源检索的错误消息。 不会转换连接数据，因为在应用程序连接到数据源之前，不会加载转换 DLL。
