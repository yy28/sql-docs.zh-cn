---
title: 默认数据源 |微软文档
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
ms.openlocfilehash: 978362b7dfe92d1333f83be684f6326cf25dd69b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305988"
---
# <a name="default-data-source"></a>默认数据源
在某些情况下，驱动程序未显式指定一个数据源，称为默认数据源：  
  
-   在调用**SQLConnect**时，*服务器名称*参数是零长度字符串、空指针或 DEFAULT。  
  
-   在**SQLDriverConnect**的调用中 *，其中 InConnectionString*指定**DSN**_DEFAULT，或者使用**DSN**关键字指定系统信息中未包含的数据源。  
  
 它是驱动程序定义的指定默认数据源的方式。 这可能涉及管理操作，并且可能取决于用户。
