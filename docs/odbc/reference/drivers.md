---
title: 驱动程序 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC]
- drivers [ODBC], about drivers
ms.assetid: d6795d92-877e-44e1-b7d5-2ff2fd3989bd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6460410488186c94713d859bf2912f2844ca2736
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915433"
---
# <a name="drivers"></a>驱动程序
*驱动程序*ODBC API 中实现的函数的库。 每个都特定于特定的 DBMS;例如，用于 Oracle 的驱动程序不能直接访问 Informix DBMS 中的数据。 驱动程序公开的功能基础 Dbms;它们不需要实现不支持的 DBMS 的功能。 例如，如果基础 DBMS 不支持外部联接中，则不应驱动程序。 仅主要的例外是不具有独立的数据库引擎，如 Xbase，Dbms 的驱动程序必须实现至少支持最少量的 SQL 数据库引擎。  
  
 本部分包含以下主题。  
  
-   [驱动程序任务](../../odbc/reference/driver-tasks.md)  
  
-   [驱动程序体系结构](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 提供的 ODBC 驱动程序](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
