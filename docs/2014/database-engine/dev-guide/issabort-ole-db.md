---
title: ISSAbort (OLE DB) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a4b3e43dca5a18a991733492eeeffc4f49d14ef8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48181237"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  **ISSAbort**接口中公开[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 提供程序提供[issabort:: Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)用于取消当前行集以及任何命令的方法进行批处理使用命令的最初生成该行集，并且，尚未完成执行。  
  
 **ISSAbort**是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过使用提供的本机客户端特定于提供程序的界面**QueryInterface**上**IMultipleResults**返回的对象**Icommand:: Execute**或**iopenrowset:: Openrowset**。  
  
## <a name="in-this-section"></a>本节内容  
  
|方法|Description|  
|------------|-----------------|  
|[Issabort:: Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|取消当前行集以及与当前命令关联的任何批处理命令。|  
  
## <a name="see-also"></a>请参阅  
 [接口&#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
