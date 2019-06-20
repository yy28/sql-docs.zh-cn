---
title: IRowsetFind 的 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability [ODBC]
ms.assetid: 7d148b56-9bbe-4e55-b31f-43f115705402
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9aa8cb118a84bca1d37bdd409055b21d1d11552
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63233021"
---
# <a name="comparability-for-irowsetfind"></a>IRowsetFind 的可比性
  IRowsetFind 支持以下比较（仅限日期/时间类型）：  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 如果试图进行其他任何比较，则将返回 DB_E_BADCOMPAREOP。 这与 OLE DB 规范是一致的。  
  
## <a name="see-also"></a>请参阅  
 [日期和时间改进 (OLE DB)](date-and-time-improvements-ole-db.md)  
  
  
