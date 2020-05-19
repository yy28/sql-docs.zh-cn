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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 39579347453fd7e40e4d8c03fe2ebb8eca3fe5a9
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704721"
---
# <a name="resynchronizing-rows"></a>重新同步行
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序仅**IRowsetResynch**支持支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 游标的行集上的 IRowsetResynch。 IRowsetResynch 并不是需要时就可用****。 使用者在打开行集前必须请求该接口。  
  
## <a name="see-also"></a>另请参阅  
 [更新行集中的数据](updating-data-in-rowsets.md)  
  
  
