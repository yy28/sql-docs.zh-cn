---
title: "更新语句限制 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UPDATE statement limitations [ODBC]
- ODBC SQL grammar, UPDATE statement limitations
ms.assetid: 14700aac-e135-4dc0-9138-4b01224461d5
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 502315916781ae5624f94e099c0cd95c52ffe8a8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="update-statement-limitations"></a>更新语句限制
Paradox 驱动程序来更新表，表必须具有唯一索引 （Paradox 主键）。 当你使用 Paradox 驱动程序而无需实现高数据库引擎时，不能更新 Paradox 表。  
  
 不支持文本驱动程序。  
  
 当使用 Microsoft Excel 驱动程序时，可以更新值，但无法从 Microsoft Excel 电子表格所基于的表中删除行。 因此，UPDATE 语句不被视为 Microsoft Excel 驱动程序正式支持。 仅 INSERT 语句被视为受支持。
