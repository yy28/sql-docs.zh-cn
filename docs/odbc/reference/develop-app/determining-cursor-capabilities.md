---
title: 确定光标功能 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], capabilities
- cursors [ODBC], scrollable
ms.assetid: 35be486c-8f2d-4cec-beb8-df14151abfef
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3974fb30a9151cdcf681a106ddcf3073b63f66b6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908962"
---
# <a name="determining-cursor-capabilities"></a>确定光标功能
中的下列四个选项**SQLGetInfo**描述了支持哪些类型的游标和其功能是什么：  
  
-   SQL_CURSOR_SENSITIVITY。 指示是否由另一个游标进行的更改对敏感游标。  
  
-   SQL_SCROLL_OPTIONS。 列出了支持的游标类型 （只进、 静态、 键集驱动、 动态的还是混合）。 所有数据源必须都支持只进游标。  
  
-   SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 （具体取决于游标的类型）。 列出支持的可滚动游标提取类型。 返回值中的位对应于在提取类型**SQLFetchScroll**。  
  
-   SQL_KEYSET_CURSOR_ATTRIBUTES2 或 SQL_STATIC_CURSOR_ATTRIBUTES2 （具体取决于游标的类型）。 列出是否静态和键集驱动游标可以检测到其自己的更新、 删除和插入。  
  
 应用程序可以确定光标功能在运行时通过调用**SQLGetInfo**使用以下选项。 这通常是通过泛型应用程序。 光标功能还可以在过程中确定应用程序开发和使用硬编码到应用程序。 这种情况通常出现由垂直和自定义应用程序，但也可以如 ODBC 游标库使用的客户端游标实现的泛型应用程序。
