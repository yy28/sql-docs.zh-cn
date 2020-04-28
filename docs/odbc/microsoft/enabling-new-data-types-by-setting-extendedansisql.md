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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b703c5c14c4743e13feee139d16e5dfeb3c24c63
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303408"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>通过设置 ExtendedAnsiSQL 启用新的数据类型
启用 ExtendedAnsiSQL 标志时，Jet 4.0 数据库中提供了两种新数据类型： SQL_DECIMAL 和 SQL_NUMERIC。 默认的精度和小数位数分别为18和0。 通过 ODBC （类型化为 SQL_DECIMAL 或 SQL_NUMERIC）访问的数据将映射到 Microsoft Jet Decimal 而不是货币。  
  
 关闭 ExtendedAnsiSQL 标志后，无法创建具有 decimal 或 numeric 类型的表，这些类型将不会出现在 SQLGetTypeInfo （）中。 但是，如果表中包含新的数据类型，则可以将它们与正确的数据类型一起使用。
