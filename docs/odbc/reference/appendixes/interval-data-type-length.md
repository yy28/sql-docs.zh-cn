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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 68bb4daa47cb58d5a0ff7b680a2d2154fb14b345
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81284315"
---
# <a name="interval-data-type-length"></a>间隔数据类型长度
以下规则用于确定间隔数据类型的长度（字符）。 长度用字符数表示。 字节数取决于字符集。 长度包含同时添加的以下值：  
  
-   间隔中的每个字段都不是前导字段，两个字符。  
  
-   对于前导字段，是表示快速或隐式前导精度的字符数。 如果未指定前导精度，则默认值为2。  
  
-   字段之间的分隔符为一个字符。  
  
-   一，加上一个表达或隐含的秒精度。 如果未指定秒精度，则默认值为6。  
  
 每个间隔数据类型的特定列长度值都包含在[列大小](../../../odbc/reference/appendixes/column-size.md)中。
