---
title: 接下来提取位置 |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6df5d3e025b16b58f105093ef64278d49f6daa78
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2018
ms.locfileid: "35694818"
---
# <a name="fetching-rows---next-fetch-position"></a>提取行-下次提取位置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序会对跟踪将下次提取位置的因此，对的调用序列**GetNextRows**方法 (而跳过，无需更改的方向，或中间调用**FindNextRow**， **Seek**，或**RestartPosition**方法) 读取整个行集，而不跳过或重复任何行。 将下次提取位置更改通过调用**irowset:: Getnextrows**， **irowset:: Restartposition**，或**IRowsetIndex::Seek**，或通过调用**FindNextRow**带 null *pBookmark*值。 调用**FindNextRow**与非空*pBookmark*值不会影响将下次提取位置。  
  
## <a name="see-also"></a>请参阅  
 [提取行](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
