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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040004"
---
# <a name="determining-cursor-capabilities"></a>确定游标功能
中的以下四个选项**SQLGetInfo**描述支持哪些类型的游标和其功能是：  
  
-   SQL_CURSOR_SENSITIVITY。 指示是否为另一个游标所做更改敏感的游标。  
  
-   SQL_SCROLL_OPTIONS。 列出了支持的游标类型 （只进、 静态、 由键集驱动、 动态的或混合）。 所有数据源必须都支持只进游标。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型）。 列出了支持可滚动游标的提取类型。 返回值中的位对应于中的提取类型**SQLFetchScroll**。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 （具体取决于游标的类型）。 列出是否静态和由键集驱动游标可以检测到其自己的更新、 删除和插入。  
  
 应用程序可以确定游标功能在运行时通过调用**SQLGetInfo**与这些选项。 这通常可通过通用应用程序。 游标功能还可确定在应用程序开发和使用硬编码到应用程序。 这通常通过在垂直和自定义应用程序，但也可以使用如 ODBC 游标库的客户端游标实现的泛型应用程序。
