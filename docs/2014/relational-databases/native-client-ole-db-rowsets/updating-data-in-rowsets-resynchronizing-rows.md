---
title: 重新同步行 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7b041dc07afb30fff0c03d96fec9cd8a5d62f965
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63229014"
---
# <a name="resynchronizing-rows"></a>重新同步行
  Native Client OLE DB 提供程序仅支持支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标的行集上的**IRowsetResynch。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] IRowsetResynch 并不是需要时就可用****。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集中的数据](updating-data-in-rowsets.md)  
  
  
