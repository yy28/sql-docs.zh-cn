---
title: 数据类型限制 |微软文档
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
ms.openlocfilehash: 4beaf91a4ead743e3e8a2e32578796baba3c17be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280667"
---
# <a name="data-type-limitations"></a>数据类型限制
Microsoft ODBC 桌面数据库驱动程序对数据类型施加了以下限制：  
  
|数据类型|描述|  
|---------------|-----------------|  
|所有数据类型|类型转换失败可能导致受影响的列设置为 NULL。|  
|BINARY|创建零长度的 BINARY 列实际上返回一个 255 字节的 BINARY 列。|  
|DATE|转换函数不能将 DATE 数据类型转换为其他数据类型（或本身）。|  
|DECIMAL（精确数字）|不支持。|  
|浮点数据类型|浮点数字中的小数位数可能受 Windows 控制面板国际部分中设置的数字格式的限制。|  
|NUMERIC|支持最大精度和 28 级。|  
|TIMESTAMP|转换函数不能将时间 STAMP 数据类型转换为自身。|  
|TINYINT|TINYINT 值始终未签名。|  
|零长度字符串|当使用 dBASE、Microsoft Excel、悖论或文本驱动程序时，将零长度字符串插入列实际上插入 NULL。|
