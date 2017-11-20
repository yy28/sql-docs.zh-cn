---
title: "通过设置 ExtendedAnsiSQL 启用新的数据类型 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5161224a5d4fe3f0bf2af200a5cff3e1ea4e1008
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>通过设置 ExtendedAnsiSQL 启用新的数据类型
ExtendedAnsiSQL 标志打开时，两个新的数据类型是在 Jet 4.0 数据库中可用： SQL_DECIMAL 和 SQL_NUMERIC。 默认值精度和小数位数分别为 18 和 0。 通过类型化为 SQL_DECIMAL 或 SQL_NUMERIC 的 ODBC 访问的数据将映射为 Microsoft Jet 十进制数字，而不是货币。  
  
 当关闭 ExtendedAnsiSQL 标志时，不能使用 decimal 或 numeric 类型，创建表，这些类型不会显示在 SQLGetTypeInfo()。 但是，如果表中包含新的数据类型，它们可与正确的数据类型。

