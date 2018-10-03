---
title: 下次提取位置 |Microsoft Docs
description: 提取行 - 下次提取位置
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: cdfe3a7c5d702bed0b40447ae196a181ed3e4e15
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731635"
---
# <a name="fetching-rows---next-fetch-position"></a>提取行 - 下次提取位置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序对下次提取位置保持跟踪，以便对 GetNextRows 方法的一系列调用（无需跳过、更改方向或干预对 FindNextRow、Seek 或 RestartPosition 方法的调用）读取整个行集，而不跳过或重复任何行。 可以通过调用 IRowset::GetNextRows、IRowset::RestartPosition 或 IRowsetIndex::Seek，或通过调用 FindNextRow 且 pBookmark 值为空来更改下次提取位置。 调用 FindNextRow 且 pBookmark 值不为空时，不会影响下次提取位置。  
  
## <a name="see-also"></a>另请参阅  
 [提取行](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
