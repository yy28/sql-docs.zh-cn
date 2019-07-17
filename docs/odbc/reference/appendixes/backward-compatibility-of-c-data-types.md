---
title: C 数据类型的向后兼容性 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dcfc4dd2ef1bee2783f073fbb85c0d911f84305a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037799"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 数据类型的后向兼容性
SQL_C_SHORT、 SQL_C_LONG 和 SQL_C_TINYINT 已替换为在 ODBC 中有符号和无符号类型：SQL_C_SSHORT 和 SQL_C_USHORT、 SQL_C_SLONG 和 SQL_C_ULONG，和 SQL_C_STINYINT 和 SQL_C_UTINYINT。 ODBC *3.x*应适用于 ODBC 的驱动程序*2.x*应用程序应支持 SQL_C_SHORT、 SQL_C_LONG 和 SQL_C_TINYINT，因为驱动程序管理器时调用，将它们到传递驱动程序。
