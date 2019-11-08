---
title: 下一次提取位置 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 632622f985e363d87cd820729afb6f69826c903b
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788983"
---
# <a name="fetching-rows---next-fetch-position"></a>提取行 - 下次提取位置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序跟踪下一个提取位置，以便对**GetNextRows**方法的调用序列（无需跳过、方向更改或干预调用**FindNextRow**、 **Seek**或**RestartPosition**方法）读取整个行集，而无需跳过或重复任何行。 可以通过调用 IRowset::GetNextRows、IRowset::RestartPosition 或 IRowsetIndex::Seek，或通过调用 FindNextRow 且 pBookmark 值为空来更改下次提取位置。 调用 FindNextRow 且 pBookmark 值不为空时，不会影响下次提取位置。  
  
## <a name="see-also"></a>另请参阅  
 [提取行](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
