---
title: 数据类型的限制 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4ce0eb96832f4a6b9c1953b0a9a9d0af65cb3b0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187443"
---
# <a name="data-type-limitations"></a>数据类型限制
Microsoft ODBC 桌面数据库驱动程序来实施对数据类型的以下限制：  
  
|数据类型|Description|  
|---------------|-----------------|  
|所有数据类型|类型转换失败可能会导致受影响的列设置为 NULL。|  
|BINARY|创建一个长度为零的二进制列实际返回 255 个字节的二进制列。|  
|DATE|DATE 数据类型不能由转换函数转换为另一种数据类型 （或本身）。|  
|小数 （精确数字）|不提供支持。|  
|浮点数据类型|在 Windows 控制面板的国际部分中设置的数字格式可能受限于的浮点数中的小数位数。|  
|NUMERIC|支持最大精度和小数位数为 28。|  
|timestamp|时间戳数据类型不能由转换函数转换为本身。|  
|TINYINT|TINYINT 值始终是无符号的。|  
|长度为零的字符串|当使用 dBASE、 Microsoft Excel、 Paradox 或 Textdriver 时，将插入列的长度为零的字符串实际上将插入 NULL 改为。|
