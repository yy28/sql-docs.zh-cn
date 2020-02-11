---
title: 转义序列 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- escape sequences [ODBC], determining if supported
- interoperability of SQL statements [ODBC], escape sequences
ms.assetid: 5913abfa-d280-43e4-a2f1-05a924388bf9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d73282cde4d0598d7e6a35ac6273935626b96969
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68001379"
---
# <a name="escape-sequences"></a>转义序列
ODBC 定义的转义序列包含日期、时间、时间戳和日期时间间隔文本、标量函数调用（**如**谓词转义符、外部联接和过程调用）的标准语法。 可互操作的应用程序应尽可能使用这些序列。  
  
 若要确定驱动程序是否支持日期、时间、时间戳或日期时间间隔文本的转义序列，应用程序将调用**SQLGetTypeInfo**。 如果数据源支持日期、时间、时间戳或日期时间间隔数据类型，则它还必须支持相应的转义序列。 若要确定是否支持其他转义序列，应用程序将调用**SQLGetInfo**。  
  
 有关详细信息，请参阅本部分后面的[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)。
