---
title: IDBProperties (OLE DB) |Microsoft 文档
description: IDBProperties 接口 (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e147d97391f823fdef2d315a6663806feea6f080
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 标准规范允许在提供程序可以指定为 VT_EMPTY **DBPROPINFO::vValues**。 但是，OLE DB 驱动程序用于 SQL Server OLE DB 始终返回 VT_EMPTY 在调用时**IDBProperties::GetPropertyInfo**与**DBPROPSET_ROWSETALL**检索行集属性。  
  
## <a name="see-also"></a>另请参阅  
 [接口 & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
