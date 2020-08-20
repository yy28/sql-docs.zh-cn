---
description: 批处理模式
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 4642a51b950c6f28566adaeccb6ddfb532d795be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88453719"
---
# <a name="batch-mode"></a>批处理模式
当 **LockType** 属性设置为 **adLockBatchOptimistic** ，并且提供程序支持批处理更新时，批处理模式有效。 某些锁类型设置不可用，具体取决于游标位置。 例如，当 **CursorLocation** 设置为 **adUseClient**时，悲观锁定类型不可用。 相反，当光标位于服务器上时，提供程序不支持批处理开放式锁定。 只应将批处理更新用于键集或静态游标。  
  
 **UpdateBatch**方法用于将复制缓冲区中保存的**记录集**更改发送到服务器以更新数据源。 在下一部分中，我们将在批处理模式下打开一个 **记录集** ，对复制缓冲区进行更改，然后通过调用 **UpdateBatch**将更改发送到数据源。  
  
 本节包含下列主题：  
  
-   [发送更新：UpdateBatch 方法](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [筛选更新的记录](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [处理失败的更新](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [检测和解决冲突](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [断开连接并重新连接记录集](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [更新已加入结果：唯一表](../../../ado/guide/data/updating-joined-results-unique-table.md)
