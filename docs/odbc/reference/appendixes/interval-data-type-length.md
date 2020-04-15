---
title: 间隔数据类型长度 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68bb4daa47cb58d5a0ff7b680a2d2154fb14b345
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284315"
---
# <a name="interval-data-type-length"></a>间隔数据类型长度
以下规则用于确定以字符为单位的间隔数据类型的长度。 长度以字符数表示。 字节数取决于字符集。 长度包括添加在一起的以下值：  
  
-   间隔中每个字段的两个字符，而不是前导字段。  
  
-   对于前导字段，表示表示或隐式前导精度的字符数。 如果未指定前导精度，则默认值为 2。  
  
-   字段之间的分隔符的一个字符。  
  
-   一加上明示或隐含秒精度。 如果未指定秒精度，则默认值为 6。  
  
 每个间隔数据类型的特定列长度值包含在[列大小](../../../odbc/reference/appendixes/column-size.md)中。
