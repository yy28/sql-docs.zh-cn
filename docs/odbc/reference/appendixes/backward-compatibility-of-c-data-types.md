---
title: C 数据类型的向后兼容性 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4a89b282a2229b6f34833b4371081661ea51b231
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304582"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 数据类型的后向兼容性
SQL_C_SHORT、SQL_C_LONG和SQL_C_TINYINT已在 ODBC 中替换为已签名和未签名的类型：SQL_C_SSHORT和SQL_C_USHORT、SQL_C_SLONG和SQL_C_ULONG以及SQL_C_STINYINT和SQL_C_UTINYINT。 应使用 ODBC *2.x*应用程序的 ODBC *3.x*驱动程序应支持SQL_C_SHORT、SQL_C_LONG和SQL_C_TINYINT，因为当调用它们时，驱动程序管理器会将它们传递给驱动程序。
