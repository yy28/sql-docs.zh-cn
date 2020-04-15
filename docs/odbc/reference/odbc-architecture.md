---
title: ODBC 架构 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07435dc1a5fbe800f2260e914f315cfe93dd8d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305128"
---
# <a name="odbc-architecture"></a>ODBC 体系结构
ODBC 体系结构有四个组件：  
  
-   **应用**执行处理并调用 ODBC 函数以提交 SQL 语句并检索结果。  
  
-   **驱动程序管理器**代表应用程序加载和卸载驱动程序。 处理 ODBC 函数调用或将其传递给驱动程序。  
  
-   **驱动程序**处理 ODBC 函数调用，向特定数据源提交 SQL 请求，并将结果返回给应用程序。 如有必要，驱动程序将修改应用程序的请求，以便请求符合关联的 DBMS 支持的语法。  
  
-   **数据源**由用户想要访问的数据及其关联的操作系统、DBMS 和网络平台（如果有）组成，用于访问 DBMS。  
  
 请注意有关 ODBC 体系结构的以下几点。 首先，可以存在多个驱动程序和数据源，这允许应用程序同时访问来自多个数据源的数据。 其次，ODBC API 在两个位置使用：在应用程序和驱动程序管理器之间，以及驱动程序管理器和每个驱动程序之间。 驱动程序管理器和驱动程序之间的接口有时称为*服务提供商接口或* *SPI*。 对于 ODBC，应用程序编程接口 （API） 和服务提供商接口 （SPI） 相同;即，驱动程序管理器和每个驱动程序具有相同的函数接口。  
  
 本部分包含以下主题。  
  
-   [应用程序](../../odbc/reference/applications.md)  
  
-   [驱动程序管理器](../../odbc/reference/the-driver-manager.md)  
  
-   [驱动程序](../../odbc/reference/drivers.md)  
  
-   [数据源](../../odbc/reference/data-sources.md)
