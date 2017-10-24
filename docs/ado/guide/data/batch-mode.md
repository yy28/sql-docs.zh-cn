---
title: "批处理模式 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 92e249a7c2d5b0c01e291f4829d5c4f8c580fb2c
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="batch-mode"></a>批处理模式
批处理模式，则当**LockType**属性设置为**adLockBatchOptimistic**和提供程序支持批处理更新。 某些锁类型设置不可用，具体取决于游标位置。 例如，保守式锁定类型不可用时**CursorLocation**设置为**adUseClient**。 相反，提供程序不能支持批处理乐观锁定，当光标位置位于服务器上时。 你应使用批处理使用的键集或仅静态游标更新。  
  
 **UpdateBatch**方法用于发送**记录集**更改保存到服务器以更新数据源在复制缓冲区中。 在以下部分中，我们将打开**记录集**在批处理模式下，对复制缓冲区中，进行更改，然后将更改发送到数据源调用**UpdateBatch**。  
  
 本节包含下列主题：  
  
-   [将更新发送： UpdateBatch 方法](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [筛选更新的记录](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [处理失败的更新](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [检测和解决冲突](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [断开连接，并重新连接记录集](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [更新已加入结果： 唯一表](../../../ado/guide/data/updating-joined-results-unique-table.md)

