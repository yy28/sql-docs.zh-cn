---
title: 重新同步行 |Microsoft 文档
description: 使用 SQL Server 的 OLE DB 驱动程序的重新同步的行
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
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
ms.openlocfilehash: cda60f254d200e6e8c23235bdeb9988b2dd80309
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>更新行集合的重新同步的行中的数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 的 OLE DB 驱动程序支持**IRowsetResynch**上[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]光标支持行集仅。 **IRowsetResynch**不是可以根据需要使用。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集合中的数据](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
