---
title: 重新同步行 |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63229014"
---
# <a name="resynchronizing-rows"></a>重新同步行
  Native Client OLE DB 提供程序仅支持支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]游标的行集上的**IRowsetResynch。** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **IRowsetResynch**不可用于点播。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集中的数据](updating-data-in-rowsets.md)  
  
  
