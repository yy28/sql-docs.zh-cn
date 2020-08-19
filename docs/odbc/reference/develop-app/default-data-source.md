---
description: 默认数据源
title: 默认数据源 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0aecd2ec64926a9d1a38d8e3d603124d45223004
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424710"
---
# <a name="default-data-source"></a>默认数据源
在应用程序未显式指定数据源的某些情况下，驱动程序可能会选择称为默认数据源的数据源：  
  
-   在对 **SQLConnect** 的调用中，其中 *ServerName* 参数是长度为零的字符串、NULL 指针或默认值。  
  
-   在对 **SQLDriverConnect** 的调用中， *InConnectionString* 指定 **dsn**= DEFAULT，或使用 **DSN** 关键字指定系统信息中未包含的数据源。  
  
 它是驱动程序定义的默认数据源的指定方式。 这可能涉及到管理操作，并且可能依赖于用户。
