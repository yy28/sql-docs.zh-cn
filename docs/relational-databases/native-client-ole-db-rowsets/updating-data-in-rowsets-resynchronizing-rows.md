---
title: 重新同步行 | Microsoft Docs
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
ms.openlocfilehash: 44e31275a6eb3ab728d1a9d7280a3d77404f7248
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300245"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>更新行集中的数据 - 重新同步行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  本机[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]客户端 OLE 数据库提供程序仅支持游标支持的行集[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上的**IRowset Resynch。** IRowsetResynch 并不是需要时就可用****。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集中的数据](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
