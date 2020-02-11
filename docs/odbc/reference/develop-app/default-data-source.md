---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fb016ac7597617b119834e20ffd9e12bd648dc0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076850"
---
# <a name="default-data-source"></a>默认数据源
在应用程序未显式指定数据源的某些情况下，驱动程序可能会选择称为默认数据源的数据源：  
  
-   在对**SQLConnect**的调用中，其中*ServerName*参数是长度为零的字符串、NULL 指针或默认值。  
  
-   在对**SQLDriverConnect**的调用中， *InConnectionString*指定**dsn**= DEFAULT，或使用**DSN**关键字指定系统信息中未包含的数据源。  
  
 它是驱动程序定义的默认数据源的指定方式。 这可能涉及到管理操作，并且可能依赖于用户。
