---
description: 数据类型限制
title: 数据类型限制 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4853846f21aa0ad763295bbdc4233c472ac53864
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412783"
---
# <a name="data-type-limitations"></a>数据类型限制
Microsoft ODBC 桌面数据库驱动程序对数据类型有以下限制：  
  
|数据类型|说明|  
|---------------|-----------------|  
|所有数据类型|如果类型转换失败，则可能导致受影响的列被设置为 NULL。|  
|BINARY|创建长度为零的二进制列实际上返回255字节的二进制列。|  
|DATE|DATE 数据类型无法转换为另一种数据类型 (或其自身) CONVERT 函数。|  
|小数 (精确数值) |不支持。|  
|浮点数据类型|浮点数中的小数位数可能受 Windows "控制面板" 的 "国际" 部分中设置的数字格式的限制。|  
|NUMERIC|支持最大精度和28的小数位数。|  
|TIMESTAMP|TIMESTAMP 数据类型不能通过 CONVERT 函数转换为自身。|  
|TINYINT|TINYINT 值始终是无符号值。|  
|长度为零的字符串|使用 dBASE、Microsoft Excel、Paradox 或 Textdriver 时，将长度为零的字符串插入列实际上是插入 NULL。|
