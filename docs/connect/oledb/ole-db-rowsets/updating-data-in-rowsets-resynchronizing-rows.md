---
title: 重新同步行 |Microsoft 文档
description: 使用 SQL Server 的 OLE DB 驱动程序的重新同步的行
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9dd0506deccd11250ed5251a18fe074325920b30
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>更新行集合的重新同步的行中的数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序支持**IRowsetResynch**上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]光标支持行集仅。 **IRowsetResynch**不是可以根据需要使用。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集合中的数据](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
