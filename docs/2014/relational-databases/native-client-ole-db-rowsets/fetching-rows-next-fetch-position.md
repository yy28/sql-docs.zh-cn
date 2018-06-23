---
title: 接下来提取位置 |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
ms.assetid: 9ef74b3f-c9c0-492f-9b93-d65738a61abd
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 59af82cea07c73f346c4c8add2cd73e3de2444cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017314"
---
# <a name="next-fetch-position"></a>下次提取位置
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序会对跟踪将下次提取位置的因此，对的调用序列**GetNextRows**方法 (而跳过，无需更改的方向，或中间调用**FindNextRow**， **Seek**，或**RestartPosition**方法) 读取整个行集，而不跳过或重复任何行。 将下次提取位置更改通过调用**irowset:: Getnextrows**， **irowset:: Restartposition**，或**IRowsetIndex::Seek**，或通过调用**FindNextRow**带 null *pBookmark*值。 调用**FindNextRow**与非空*pBookmark*值不会影响将下次提取位置。  
  
## <a name="see-also"></a>请参阅  
 [提取行](fetching-rows.md)  
  
  