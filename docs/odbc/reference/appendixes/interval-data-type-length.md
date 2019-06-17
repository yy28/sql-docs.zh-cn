---
title: 间隔数据类型长度 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16d0590d3297b52891bf399822ce984674022583
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188917"
---
# <a name="interval-data-type-length"></a>间隔数据类型长度
以下规则用于确定以字符为单位的时间间隔数据类型的长度。 中的字符数表示长度。 字节数取决于的字符集。 长度包括加在一起的以下值：  
  
-   不是前导字段的时间间隔中每个字段的两个字符。  
  
-   对于前导字段，或隐式前导精度的字符数。 如果未指定前导精度，默认值为 2。  
  
-   一个字符的字段之间的分隔符。  
  
-   加一的明示或暗示的秒精度。 如果未指定的秒精度，默认值为 6。  
  
 中包含的每个间隔数据类型的特定列长度值[列大小](../../../odbc/reference/appendixes/column-size.md)。
