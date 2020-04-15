---
title: 确定光标功能 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 984ad8302f2e1695c8df84a64a18042f4cc9e364
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305878"
---
# <a name="determining-cursor-capabilities"></a>确定游标功能
**SQLGetInfo**中的以下四个选项描述了支持哪些类型的游标及其功能：  
  
-   SQL_CURSOR_SENSITIVITY 指示游标是否对另一个游标所做的更改敏感。  
  
-   SQL_SCROLL_OPTIONS 列出支持的游标类型（仅转发、静态、键集驱动、动态或混合）。 所有数据源都必须支持仅转发游标。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1（取决于光标的类型）。 列出可滚动游标支持的提取类型。 返回值中的位对应于**SQLFetchScroll**中的提取类型。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2或SQL_STATIC_CURSOR_ATTRIBUTES2（取决于光标的类型）。 列出静态和按键集驱动的游标是否可以检测自己的更新、删除和插入。  
  
 应用程序可以通过使用这些选项调用**SQLGetInfo**来确定运行时的游标功能。 这通常由通用应用程序完成。 光标功能也可以在应用程序开发期间确定，并在应用程序中硬编码使用。 这通常由垂直和自定义应用程序完成，但也可以通过使用客户端游标实现的泛型应用程序（如 ODBC 游标库）来完成。
