---
title: 通过设置 ExtendedAnsiSQL 启用新的数据类型 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- extendedANSISQL [ODBC], enabling new data types
ms.assetid: f2865543-7fff-44fa-9a6a-968bec33acdc
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88f11adcab09dbe6964bfd67a944912fc185bccb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68031117"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>通过设置 ExtendedAnsiSQL 启用新的数据类型
ExtendedAnsiSQL 标志开启时，两个新的数据类型为 Jet 4.0 数据库中可用：SQL_DECIMAL 和 SQL_NUMERIC。 默认精度和小数位数分别为 18 和 0。 通过 ODBC 类型 SQL_DECIMAL 或 SQL_NUMERIC 为访问的数据将映射为 Microsoft Jet 十进制数字，而不是货币。  
  
 当 ExtendedAnsiSQL 标志处于关闭状态时，不能使用 decimal 或 numeric 类型创建表和这些类型不会出现在 SQLGetTypeInfo()。 但是，如果表包含新的数据类型，它们可以在正确的数据类型。
