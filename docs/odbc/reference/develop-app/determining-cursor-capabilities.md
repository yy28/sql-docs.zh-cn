---
title: 确定游标功能 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14715e40cd99f3f1a03c2ae19e825705a8376e30
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68040004"
---
# <a name="determining-cursor-capabilities"></a>确定游标功能
**SQLGetInfo**中的以下四个选项描述支持的游标类型及其功能：  
  
-   SQL_CURSOR_SENSITIVITY。 指示游标是否对其他游标所做的更改敏感。  
  
-   SQL_SCROLL_OPTIONS。 列出支持的游标类型（只进、静态、键集驱动、动态或混合）。 所有数据源都必须支持只进游标。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型）。 列出可滚动游标支持的提取类型。 返回值中的位对应于**SQLFetchScroll**中的提取类型。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 （取决于游标的类型）。 列出了静态游标和由键集驱动的游标是否可以检测到其自己的更新、删除和插入操作。  
  
 应用程序可以通过使用这些选项调用**SQLGetInfo**来确定运行时的游标功能。 通常由一般应用程序完成此操作。 还可在应用程序开发过程中确定游标功能，并在应用程序中对其进行硬编码。 这通常是由垂直和自定义应用程序完成的，但也可以通过使用客户端游标实现的泛型应用程序（如 ODBC 游标库）来实现。
