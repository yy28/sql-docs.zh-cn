---
title: 转换 Dll |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ec1d0e23019f3e5b68ad38711c1f041b160ceb31
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47833855"
---
# <a name="translation-dlls"></a>转换 DLL
应用程序和数据源通常将数据存储在不同的字符集。 ODBC 提供了将允许驱动程序将数据从设置到另一个字符转换的通用机制。 它包含实现的转换函数的 DLL **SQLDriverToDataSource**并**SQLDataSourceToDriver**，由驱动程序进行转换的数据源之间流动的所有数据调用和驱动程序。 此 DLL 可由应用程序开发人员，驱动程序开发人员，编写或第三方。  
  
 可以在该数据源; 的系统信息中指定特定数据源的转换 DLL有关详细信息，请参阅[数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)。 它还可以将设置在运行时使用 SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION 连接属性。  
  
 翻译选项是一个值，可以仅由特定转换 DLL 解释该值。 例如，如果转换 DLL 为转换之间不同的代码页中，选项可能会给应用程序和数据源使用的代码页的数字。 没有为翻译 DLL 要求使用转换选项。  
  
 后进行转换时指定的 DLL，该驱动程序将其加载并调用它将转换应用程序和数据源之间流动的所有数据。 这包括所有 SQL 语句和字符参数发送到数据源，以及从数据源中检索所有字符都会、 字符元数据，例如列名称和错误消息。 连接数据未被转换，因为该应用程序具有连接到数据源后不直到加载转换 DLL。
