---
title: 通过设置 ExtendedAnsiSQL 启用新的数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4c9f7c4c66bebb2404ef8477ed85e0f36edc1407
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>通过设置 ExtendedAnsiSQL 启用新的数据类型
ExtendedAnsiSQL 标志打开时，两个新的数据类型是在 Jet 4.0 数据库中可用： SQL_DECIMAL 和 SQL_NUMERIC。 默认值精度和小数位数分别为 18 和 0。 通过类型化为 SQL_DECIMAL 或 SQL_NUMERIC 的 ODBC 访问的数据将映射为 Microsoft Jet 十进制数字，而不是货币。  
  
 当关闭 ExtendedAnsiSQL 标志时，不能使用 decimal 或 numeric 类型，创建表，这些类型不会显示在 SQLGetTypeInfo()。 但是，如果表中包含新的数据类型，它们可与正确的数据类型。
