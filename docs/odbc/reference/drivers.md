---
description: 驱动程序
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 81e8989fc178728e687baa13b37e6055692d9413
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494590"
---
# <a name="drivers"></a>驱动程序
*驱动程序* 是在 ODBC API 中实现函数的库。 每个专用于特定的 DBMS;例如，Oracle 驱动程序无法直接访问 Informix DBMS 中的数据。 驱动程序公开底层 Dbms 的功能;它们不需要实现 DBMS 不支持的功能。 例如，如果基础 DBMS 不支持外部联接，则这两个驱动程序都不应。 唯一要注意的是，没有独立数据库引擎（如 Xbase）的 Dbms 驱动程序必须实现至少支持最少数量的 SQL 的数据库引擎。  
  
 本部分包含以下主题。  
  
-   [驱动程序任务](../../odbc/reference/driver-tasks.md)  
  
-   [驱动程序体系结构](../../odbc/reference/driver-architecture.md)  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft 提供的 ODBC 驱动程序](../../odbc/microsoft/microsoft-supplied-odbc-drivers.md)
