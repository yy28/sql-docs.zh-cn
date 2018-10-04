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
manager: craigg
ms.openlocfilehash: 909f9b3e7c8087add8eb66ca2f5c15253026304c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619565"
---
# <a name="default-data-source"></a>默认数据源
该驱动程序可能会选择名为默认数据源，在某些情况下，其中应用程序没有显式指定一个数据源：  
  
-   在调用**SQLConnect**其中*ServerName*参数是一个零长度字符串、 null 指针或默认值。  
  
-   在调用**SQLDriverConnect**其中*InConnectionString*或者指定**DSN**= 默认值或指定具有**DSN**关键字未包含在系统信息的数据源。  
  
 它是驱动程序定义指定的默认数据源的方式。 这可能涉及到管理操作，并可能取决于用户。
