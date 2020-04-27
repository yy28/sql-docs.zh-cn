---
title: ISSAbort （OLE DB） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- ISSAbort interface
ms.assetid: 7c4df482-4a83-4da0-802b-3637b507693a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 801eb84df08837ec8e49b6bb0e28fc1f1115e674
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "62781033"
---
# <a name="issabort-ole-db"></a>ISSAbort (OLE DB)
  在**ISSAbort** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 提供程序中公开的 ISSAbort 接口提供[ISSAbort：： Abort](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)方法，该方法用于取消当前行集以及使用最初生成了行集的命令进行批处理，并且尚未完成执行的任何命令。  
  
 **ISSAbort**是一[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]种特定于 Native Client 提供程序的接口，可通过对**ICommand：： Execute**或**IOpenRowset：： OpenRowset**返回的**IMultipleResults**对象使用**QueryInterface** 。  
  
## <a name="in-this-section"></a>本节内容  
  
|方法|说明|  
|------------|-----------------|  
|[ISSAbort：： Abort &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/issabort-abort-ole-db.md)|取消当前行集以及与当前命令关联的任何批处理命令。|  
  
## <a name="see-also"></a>另请参阅  
 [接口 &#40;OLE DB&#41;](../../../2014/database-engine/dev-guide/interfaces-ole-db.md)  
  
  
