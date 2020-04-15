---
title: 通过设置扩展安西SQL 启用新数据类型 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303408"
---
# <a name="enabling-new-data-types-by-setting-extendedansisql"></a>通过设置 ExtendedAnsiSQL 启用新的数据类型
打开扩展安西SQL 标志时，Jet 4.0 数据库中有两种新的数据类型：SQL_DECIMAL和SQL_NUMERIC。 默认精度和比例分别为 18 和 0。 通过 ODBC 访问的数据键入为SQL_DECIMAL或SQL_NUMERIC将映射到 Microsoft Jet 十进制，而不是货币。  
  
 关闭扩展 AnsiSQL 标志后，无法创建具有小数或数字类型的表，并且这些类型将不会显示在 SQLGetTypeInfo（） 中。 但是，如果表包含新的数据类型，则可以将它们与正确的数据类型一起使用。
