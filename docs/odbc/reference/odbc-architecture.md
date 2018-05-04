---
title: ODBC 体系结构 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], components
- ODBC architecture [ODBC]
ms.assetid: 2604f492-587b-4a51-9876-59a7870b3ef2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 59076df0044feea340c54df8af78bc286afba96b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-architecture"></a>ODBC 体系结构
ODBC 体系结构具有四个组件：  
  
-   **应用程序**执行处理和调用 ODBC 函数以提交 SQL 语句和检索结果。  
  
-   **驱动程序管理器**加载和卸载代表应用程序的驱动程序。 进程 ODBC 函数调用，或将其传递给驱动程序。  
  
-   **驱动程序**进程 ODBC 函数调用、 SQL 将请求提交到特定数据源，并返回到应用程序的结果。 如有必要，该驱动程序将修改应用程序的请求，以便请求符合支持的关联 DBMS 语法。  
  
-   **数据源**数据-包含用户想要将访问权限和其关联的操作系统 DBMS，并且网络平台 （如果有） 用于访问 DBMS。  
  
 请注意有关 ODBC 体系结构的以下几点。 第一个、 多个驱动程序和数据源可以存在，这样，应用程序同时从多个数据源访问数据。 其次，在两个位置使用 ODBC API： 应用程序和驱动程序管理器，之间和驱动程序管理器和每个驱动程序之间。 驱动程序管理器和驱动程序之间的接口有时称为*服务提供程序接口*或*SPI*。 适用于 ODBC 应用程序编程接口 (API) 和服务提供程序接口 (SPI) 都相同;这就是，驱动程序管理器和每个驱动程序具有相同的功能的相同接口。  
  
 本部分包含以下主题。  
  
-   [应用程序](../../odbc/reference/applications.md)  
  
-   [驱动程序管理器](../../odbc/reference/the-driver-manager.md)  
  
-   [驱动程序](../../odbc/reference/drivers.md)  
  
-   [数据源](../../odbc/reference/data-sources.md)
