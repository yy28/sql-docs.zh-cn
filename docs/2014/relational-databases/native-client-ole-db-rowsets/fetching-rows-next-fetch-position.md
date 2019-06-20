---
title: 下次提取位置 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 2c47f1a8692cf7d2e3fb4f00c64770b3b0c69e5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63183641"
---
# <a name="next-fetch-position"></a>下次提取位置
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序保留对其进行跟踪的下次提取位置因此对的调用序列**GetNextRows**方法 (而无需跳过，方向或干预性的更改调用**FindNextRow**， **Seek**，或**RestartPosition**方法) 读取整个行集，而无需跳过或重复任何行。 可以通过调用 IRowset::GetNextRows、IRowset::RestartPosition 或 IRowsetIndex::Seek，或通过调用 FindNextRow 且 pBookmark 值为空来更改下次提取位置      。 调用 FindNextRow 且 pBookmark 值不为空时，不会影响下次提取位置   。  
  
## <a name="see-also"></a>请参阅  
 [提取行](fetching-rows.md)  
  
  
