---
description: C 数据类型的后向兼容性
title: C 数据类型的后向兼容性 |Microsoft Docs
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
ms.openlocfilehash: e50a07d3c49438fcdfbc0b57ec70380d20c88440
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411313"
---
# <a name="backward-compatibility-of-c-data-types"></a>C 数据类型的后向兼容性
已通过签名和无符号类型在 ODBC 中替换 SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT： SQL_C_SSHORT 和 SQL_C_USHORT、SQL_C_SLONG 和 SQL_C_ULONG 以及 SQL_C_STINYINT 和 SQL_C_UTINYINT。 应使用 *odbc 2.x* *应用程序的 odbc* 2.x 驱动程序应支持 SQL_C_SHORT、SQL_C_LONG 和 SQL_C_TINYINT，因为调用它们时，驱动程序管理器会将它们传递给驱动程序。
