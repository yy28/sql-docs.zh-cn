---
title: "转换 Dll |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- translation DLLs [ODBC]
ms.assetid: 38975059-b346-410f-bb27-326f3f7bbf39
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06e496e3999904a019f481374598a9a774729ab3
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="translation-dlls"></a>转换 Dll
应用程序和数据源通常将数据存储在不同的字符集。 ODBC 提供允许驱动程序会将数据从一个字符设置为另一个转换的泛型机制。 它包含实现的转换函数的 DLL **SQLDriverToDataSource**和**SQLDataSourceToDriver**，要将所有的数据源之间流动的数据转换的驱动程序时会调用它和驱动程序。 此 DLL 可由应用程序开发人员，驱动程序开发人员编写或第三方。  
  
 可以在该数据源; 的系统信息中指定特定数据源的转换 DLL有关详细信息，请参阅[数据源规范子项](../../../odbc/reference/install/data-source-specification-subkeys.md)。 它可以也设置在运行时的 SQL_ATTR_TRANSLATE_DLL 和 SQL_ATTR_TRANSLATE_OPTION 连接属性。  
  
 转换选项是一个值，可以仅由特定转换 DLL 解释。 例如，如果转换 DLL 将转换之间不同的代码页中，选项可能会产生应用程序和数据源使用的代码页的数目。 没有为翻译 DLL 要求必须使用转换选项。  
  
 后指定 DLL 进行转换时，该驱动程序来加载它并调用它会将所有应用程序和数据源之间流动的数据转换。 这包括所有 SQL 语句和字符参数发送到数据源，以及从数据源中检索所有字符结果、 字符元数据，例如列名称，以及错误消息。 连接数据不会进行转换，因为后应用程序已连接到数据源不直到加载转换 DLL。

