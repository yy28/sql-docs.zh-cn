---
title: 重新同步行（Native Client OLE DB 提供程序）
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e260334701d49f31e42a289e08c3938955ce4fcd
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87393585"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows-in-sql-server-native-client"></a>更新行集中的数据-重新同步 SQL Server Native Client 中的行
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序仅**IRowsetResynch**支持支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标的行集上的 IRowsetResynch。 IRowsetResynch 并不是需要时就可用****。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集中的数据](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
