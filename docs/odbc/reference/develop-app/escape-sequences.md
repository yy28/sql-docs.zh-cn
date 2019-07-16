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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68001379"
---
# <a name="escape-sequences"></a>转义序列
ODBC 定义包含日期、 时间、 时间戳和日期时间间隔文字标量函数调用的标准语法的转义序列**如**谓词转义字符、 外部联接和过程调用。 可互操作应用程序应使用尽可能这些序列。  
  
 若要确定驱动程序是否支持针对日期、 时间、 时间戳或日期时间间隔文字的转义序列，应用程序调用**SQLGetTypeInfo**。 如果数据源支持日期、 时间、 时间戳或日期时间间隔数据类型，它还必须支持相应的转义序列。 若要确定是否支持其他转义序列，应用程序调用**SQLGetInfo**。  
  
 有关详细信息，请参阅[ODBC 中的转义序列](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md)，在本部分中更高版本。
