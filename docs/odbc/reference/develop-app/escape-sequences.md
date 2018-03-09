---
title: "转义序列 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed7759322501a8bbf7a214669c7e4c1480af8882
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="escape-sequences"></a>转义序列
ODBC 定义包含针对日期、 时间、 时间戳，和日期时间间隔文本、 标量函数调用，标准语法的转义序列**如**谓词转义字符、 外部联接中和过程调用。 可互操作的应用程序应使用尽可能这些序列。  
  
 若要确定是否驱动程序还支持针对日期、 时间、 时间戳，或日期时间间隔文本中的转义序列，应用程序调用**SQLGetTypeInfo**。 如果数据源支持日期、 时间、 时间戳或日期时间间隔数据类型，它还必须支持相应的转义序列。 若要确定是否支持的其他转义序列，应用程序调用**SQLGetInfo**。  
  
 有关详细信息，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)，本部分中更高版本。
