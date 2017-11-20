---
title: "数据类型限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 558789a4f435e9fc54176b1423d71369f6b4cc22
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="data-type-limitations"></a>数据类型限制
Microsoft ODBC 桌面数据库驱动程序施加对数据类型的以下限制：  
  
|数据类型|Description|  
|---------------|-----------------|  
|所有数据类型|类型转换失败可能会导致受影响的列设置为 NULL。|  
|BINARY|创建一个零长度的二进制列实际返回 255 字节的二进制列。|  
|DATE|日期数据类型无法转换为另一种数据类型 （或本身） 中，通过 CONVERT 函数。|  
|十进制 （精确数字）|不提供支持。|  
|浮点数据类型|通过在 Windows 控制面板的国际部分中设置的数字格式，可能仅限于的浮点数中的小数位数。|  
|NUMERIC|支持最大精度和小数位数为 28。|  
|timestamp|时间戳数据类型无法由 CONVERT 函数转换为其自身。|  
|TINYINT|TINYINT 值始终是无符号的。|  
|零长度字符串|当使用 dBASE、 Microsoft Excel、 Paradox 或 Textdriver 时，将一个零长度字符串插入列实际上将插入 NULL 改为。|

