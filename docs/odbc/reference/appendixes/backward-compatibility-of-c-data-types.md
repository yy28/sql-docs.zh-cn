---
title: 向后兼容性的 C 数据类型 |Microsoft 文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- backward compatibility [ODBC], C data types
- compatibility [ODBC], C data types
- data types [ODBC], backward compatibility
- C data types [ODBC], backward compatibility
ms.assetid: b1453a65-ae03-4061-b0cf-a8434d8bc40b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b4a4e8679596c1b2bca9aed13ff548373a7450f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="backward-compatibility-of-c-data-types"></a>向后兼容性的 C 数据类型
SQL_C_SHORT、 SQL_C_LONG 和 SQL_C_TINYINT 已替换为在 ODBC 中有符号和无符号类型： SQL_C_SSHORT 和 SQL_C_USHORT、 SQL_C_SLONG 和 SQL_C_ULONG，和 SQL_C_STINYINT 和 SQL_C_UTINYINT。 ODBC 3*.x*驱动程序都应适用于 ODBC 2。*x*应用程序应支持 SQL_C_SHORT、 SQL_C_LONG 和 SQL_C_TINYINT，因为它们调用时，驱动程序管理器将其传递通过给驱动程序。
