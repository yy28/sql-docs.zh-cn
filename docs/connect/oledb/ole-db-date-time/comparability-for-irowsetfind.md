---
title: IRowsetFind 的比较 |Microsoft 文档
description: IRowsetFind 的可比性
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b49a02e04ab8be0768695489b6423c9cc7bb941e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="comparability-for-irowsetfind"></a>IRowsetFind 的可比性
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  IRowsetFind 支持以下比较（仅限日期/时间类型）：  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 如果试图进行其他任何比较，则将返回 DB_E_BADCOMPAREOP。 这与 OLE DB 规范是一致的。  
  
## <a name="see-also"></a>另请参阅  
 [日期和时间改进 & #40; OLE DB & #41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
