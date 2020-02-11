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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68031117"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>通过设置 ExtendedAnsiSQL 启用新的数据类型
启用 ExtendedAnsiSQL 标志时，Jet 4.0 数据库中提供了两种新数据类型： SQL_DECIMAL 和 SQL_NUMERIC。 默认的精度和小数位数分别为18和0。 通过 ODBC （类型化为 SQL_DECIMAL 或 SQL_NUMERIC）访问的数据将映射到 Microsoft Jet Decimal 而不是货币。  
  
 关闭 ExtendedAnsiSQL 标志后，无法创建具有 decimal 或 numeric 类型的表，这些类型将不会出现在 SQLGetTypeInfo （）中。 但是，如果表中包含新的数据类型，则可以将它们与正确的数据类型一起使用。
