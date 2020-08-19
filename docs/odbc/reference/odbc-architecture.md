---
description: ODBC 体系结构
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3afeb698d7eff9d09161a091e3de0194fea93ec2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428999"
---
# <a name="odbc-architecture"></a>ODBC 体系结构
ODBC 体系结构具有四个组件：  
  
-   **应用程序** 执行处理并调用 ODBC 函数以提交 SQL 语句并检索结果。  
  
-   **驱动程序管理器** 代表应用程序加载和卸载驱动程序。 处理 ODBC 函数调用或将其传递给驱动程序。  
  
-   **驱动程序** 处理 ODBC 函数调用，将 SQL 请求提交到特定数据源，并将结果返回到应用程序。 如有必要，驱动程序会修改应用程序的请求，以便请求符合关联 DBMS 支持的语法。  
  
-   **数据源** 包含用户要访问的数据及其关联的操作系统、DBMS 和网络平台 (如果任何) 用于访问 DBMS。  
  
 请注意有关 ODBC 体系结构的以下几点。 首先，可以存在多个驱动程序和数据源，从而使应用程序能够同时访问多个数据源中的数据。 其次，ODBC API 在两个位置使用：在应用程序和驱动程序管理器之间，以及在驱动程序管理器和每个驱动程序之间。 驱动程序管理器和驱动程序之间的接口有时称为 *服务提供程序接口* 或 *SPI*。 对于 ODBC，应用程序编程接口 (API) 和服务提供商接口 (SPI) 相同;也就是说，驱动程序管理器和每个驱动程序对相同的函数具有相同的接口。  
  
 本部分包含以下主题。  
  
-   [应用程序](../../odbc/reference/applications.md)  
  
-   [驱动程序管理器](../../odbc/reference/the-driver-manager.md)  
  
-   [驱动程序](../../odbc/reference/drivers.md)  
  
-   [数据源](../../odbc/reference/data-sources.md)
