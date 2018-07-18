---
title: 下次提取位置 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
ms.openlocfilehash: 0b3bb59d06f0ac6b12ac9ca2f6785659a16e0e11
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426326"
---
# <a name="fetching-rows---next-fetch-position"></a>提取行-下次提取位置
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序保留对其进行跟踪的下次提取位置因此对的调用序列**GetNextRows**方法 (而无需跳过，方向或干预性的更改调用**FindNextRow**， **Seek**，或**RestartPosition**方法) 读取整个行集，而无需跳过或重复任何行。 通过调用更改下次提取位置**irowset:: Getnextrows**， **irowset:: Restartposition**，或**irowsetindex:: Seek**，或通过调用**FindNextRow**带 null *pBookmark*值。 调用**FindNextRow**的非 null *pBookmark*值不会影响下次提取位置。  
  
## <a name="see-also"></a>请参阅  
 [提取行](../../relational-databases/native-client-ole-db-rowsets/fetching-rows.md)  
  
  
