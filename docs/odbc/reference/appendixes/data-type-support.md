---
title: "数据类型支持 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 147e940dcd37b452e1fe05b3a39f6b184c810397
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-support"></a>数据类型支持
ODBC 驱动程序必须支持 SQL_CHAR 和 SQL_VARCHAR 中至少一个。 由驱动程序的或数据源的 SQL 92 一致性级别确定对其他数据类型的支持。 应用程序应调用**SQLGetTypeInfo**来确定由驱动程序支持的数据类型。  
  
 数据类型的详细信息，请参阅[附录 d： 数据类型](../../../odbc/reference/appendixes/appendix-d-data-types.md)。
