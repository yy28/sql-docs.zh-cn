---
title: 数据类型支持 |Microsoft 文档
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
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9930e89eb3f983afa8034b23cbbed69ddb985a51
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="data-type-support"></a>数据类型支持
ODBC 驱动程序必须支持 SQL_CHAR 和 SQL_VARCHAR 中至少一个。 由驱动程序的或数据源的 SQL 92 一致性级别确定对其他数据类型的支持。 应用程序应调用**SQLGetTypeInfo**来确定由驱动程序支持的数据类型。  
  
 数据类型的详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
