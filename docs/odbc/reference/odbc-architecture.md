---
title: ODBC 体系结构 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83e35d58d180336c349e83c7991d27f7007aca4e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47752845"
---
# <a name="odbc-architecture"></a>ODBC 体系结构
ODBC 体系结构具有四个组件：  
  
-   **应用程序**执行提交 SQL 语句并检索结果的处理和调用 ODBC 函数。  
  
-   **驱动程序管理器**加载和卸载驱动程序代表应用程序。 过程 ODBC 函数调用，或将其传递给驱动程序。  
  
-   **驱动程序**进程 ODBC 函数调用，将提交到特定的数据源，SQL 请求并返回到应用程序的结果。 如有必要，驱动程序将修改应用程序的请求，以便请求符合相关联的 DBMS 支持的语法。  
  
-   **数据源**的数据-包含用户想要访问和其关联的操作系统，DBMS，并且网络平台 （如果有） 用于访问 DBMS。  
  
 请注意 ODBC 体系结构有关的以下几点。 第一个、 多个驱动程序和数据源可以存在，它允许应用程序同时从多个数据源访问数据。 其次，在两个位置使用 ODBC API： 应用程序和驱动程序管理器中，驱动程序管理器和每个驱动程序之间以及之间。 驱动程序管理器和驱动程序之间的接口有时称为*服务提供程序接口*或*SPI*。 适用于 ODBC 的应用程序编程接口 (API) 和服务提供程序接口 (SPI) 都相同;也就是说，驱动程序管理器和每个驱动程序具有相同的函数相同的接口。  
  
 本部分包含以下主题。  
  
-   [应用程序](../../odbc/reference/applications.md)  
  
-   [驱动程序管理器](../../odbc/reference/the-driver-manager.md)  
  
-   [驱动程序](../../odbc/reference/drivers.md)  
  
-   [数据源](../../odbc/reference/data-sources.md)
