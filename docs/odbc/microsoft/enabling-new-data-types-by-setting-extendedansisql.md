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
manager: craigg
ms.openlocfilehash: 80a86ef188796883e76c6d5f6149a3e40afd341b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63128008"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>通过设置 ExtendedAnsiSQL 启用新的数据类型
ExtendedAnsiSQL 标志开启时，两个新的数据类型为 Jet 4.0 数据库中可用：SQL_DECIMAL 和 SQL_NUMERIC。 默认精度和小数位数分别为 18 和 0。 通过 ODBC 类型 SQL_DECIMAL 或 SQL_NUMERIC 为访问的数据将映射为 Microsoft Jet 十进制数字，而不是货币。  
  
 当 ExtendedAnsiSQL 标志处于关闭状态时，不能使用 decimal 或 numeric 类型创建表和这些类型不会出现在 SQLGetTypeInfo()。 但是，如果表包含新的数据类型，它们可以在正确的数据类型。
