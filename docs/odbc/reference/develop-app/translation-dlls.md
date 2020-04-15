---
title: 翻译 DLL |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297942"
---
# <a name="translation-dlls"></a>转换 DLL
应用程序和数据源通常将数据存储在不同的字符集中。 ODBC 提供了一种通用机制，允许驱动程序将数据从一个字符集转换为另一个字符集。 它由 DLL 组成，它实现了转换函数**SQLDriverToDataSource**和**SQLDataSourceToDriver，** 驱动程序调用它们来转换数据源和驱动程序之间的所有数据。 此 DLL 可以由应用程序开发人员、驱动程序开发人员或第三方编写。  
  
 可以在该数据源的系统信息中指定特定数据源的转换 DLL;有关详细信息，请参阅[数据源规范子密钥](../../../odbc/reference/install/data-source-specification-subkeys.md)。 也可以在运行时使用SQL_ATTR_TRANSLATE_DLL和SQL_ATTR_TRANSLATE_OPTION连接属性进行设置。  
  
 翻译选项是只能由特定翻译 DLL 解释的值。 例如，如果转换 DLL 在不同的代码页之间进行转换，则该选项可能会给出应用程序和数据源使用的代码页的数量。 无需翻译 DLL 使用翻译选项。  
  
 指定转换 DLL 后，驱动程序将加载它并调用它来转换应用程序和数据源之间的所有数据。 这包括发送到数据源的所有 SQL 语句和字符参数，以及所有字符结果、字符元数据（如列名）以及从数据源检索的错误消息。 连接数据不会翻译，因为转换 DLL 直到应用程序连接到数据源后才会加载。
