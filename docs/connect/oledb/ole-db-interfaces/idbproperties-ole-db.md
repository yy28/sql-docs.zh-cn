---
title: IDBProperties (OLE DB driver) | Microsoft Docs
description: IDBProperties 接口 (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: afaf7fc8e0ea60a1ee8576e0afa5b279653a2272
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "87244485"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 标准规范允许提供程序为 DBPROPINFO::vValues 指定 VT_EMPTY  。 但是，在使用 DBPROPSET_ROWSETALL 调用 IDBProperties::GetPropertyInfo 来检索行集属性时，OLE DB Driver for SQL Server OLE DB 始终返回 VT_EMPTY。  
  
## <a name="see-also"></a>另请参阅  
 [接口 (OLE DB)](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
