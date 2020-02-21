---
title: 重新同步行 | Microsoft Docs
description: 使用 OLE DB Driver for SQL Server 重新同步行
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2f1ea1a563e986914c5fe820740776da129c3b28
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2020
ms.locfileid: "67994170"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>更新行集中的数据 - 重新同步行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 仅对于 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 游标支持的行集支持 IRowsetResynch  。 IRowsetResynch 并不是需要时就可用  。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集中的数据](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
