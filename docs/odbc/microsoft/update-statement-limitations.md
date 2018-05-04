---
title: 更新语句限制 |Microsoft 文档
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
ms.topic: conceptual
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbb1e6cbf0660f7b016391d5881b77d7e89e1f81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="update-statement-limitations"></a>更新语句限制
Paradox 驱动程序来更新表，表必须具有唯一索引 （Paradox 主键）。 当你使用 Paradox 驱动程序而无需实现高数据库引擎时，不能更新 Paradox 表。  
  
 不支持文本驱动程序。  
  
 当使用 Microsoft Excel 驱动程序时，可以更新值，但无法从 Microsoft Excel 电子表格所基于的表中删除行。 因此，UPDATE 语句不被视为 Microsoft Excel 驱动程序正式支持。 仅 INSERT 语句被视为受支持。
