---
title: 支持的数据类型（可视化福克斯Pro ODBC驱动程序） |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fc28464a7c14f9801473cc125b0e90c50247d68
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301097"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>支持的数据类型（Visual FoxPro ODBC 驱动程序）
驱动程序支持的数据类型列表通过 ODBC API 和 Microsoft 查询显示。  
  
## <a name="data-types-in-c-applications"></a>C 应用程序中的数据类型  
 通过使用 C 或C++应用程序中的[SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md)函数，您可以获取 Visual FoxPro ODBC 驱动程序支持的数据类型列表。  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>使用 Microsoft 查询的应用程序中的数据类型  
 如果应用程序使用 Microsoft 查询在 Visual FoxPro 数据源上创建新表，则 Microsoft 查询将显示 **"新表定义"** 对话框。 在**字段描述**下，"**类型"** 框列出了由单个字符表示[的 Visual FoxPro 字段数据类型](../../odbc/microsoft/visual-foxpro-field-data-types.md)。
