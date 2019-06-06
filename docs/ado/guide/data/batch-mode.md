---
title: 批处理模式 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 39130be0e6be31700f70002726f3aaf674aa4c82
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700927"
---
# <a name="batch-mode"></a>批处理模式
批处理模式，则当**LockType**属性设置为**adLockBatchOptimistic**和提供程序支持批更新。 某些锁类型设置不可用，具体取决于游标位置。 例如，保守式锁定类型时不可用**CursorLocation**设置为**adUseClient**。 相反，提供程序不能支持批处理乐观锁定时光标所在的位置是在服务器上。 你应使用批处理使用 keyset 或 static 游标仅更新。  
  
 **UpdateBatch**方法用于发送**记录集**更改保存到服务器以更新数据源在复制缓冲区。 在以下部分中，我们将打开**记录集**在批处理模式下对复制缓冲区中，进行更改，然后将更改发送到数据源通过调用**UpdateBatch**。  
  
 本节包含下列主题：  
  
-   [发送更新：UpdateBatch 方法](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [筛选更新的记录](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [处理失败的更新](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [检测和解决冲突](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [断开连接并重新连接记录集](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [更新已加入结果：唯一表](../../../ado/guide/data/updating-joined-results-unique-table.md)
