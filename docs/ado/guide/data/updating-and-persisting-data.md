---
title: "更新和持久化数据 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b6b67b559f31dc2e7c57f32abb4a2c2e26e0e558
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="updating-and-persisting-data"></a>更新并将数据保存
前面几章讨论了如何使用 ADO 来访问数据源中的数据、 如何在数据移动和甚至如何编辑数据。 当然，如果你的应用程序的目的是允许用户对数据进行更改，你将需要了解如何保存这些更改。 您也可以保留**记录集**更改为文件使用**保存**方法，或者可以将发送所做的更改回存储使用的数据源**更新**或**UpdateBatch**方法。  
  
 以前面的章节中，更改中的多个行的数据**记录集**。 ADO 支持添加、 删除和修改的数据行与相关的两个基本概念。  
  
 第一个理念是对不立即进行更改**记录集**; 相反，它们由到内部*复制缓冲区*。 如果你决定你不希望所做的更改，复制缓冲区中的修改将被丢弃。 如果你决定要保留所做的更改，复制缓冲区中的更改应用于**记录集**。  
  
 第二个理念是，更改可以传播到数据源将工作声明行上完成时，就会立即 (即，*即时*模式)，或对一组行的所有更改都收集直到声明集的工作完成 (即，*批处理*模式)。 **LockType**属性确定何时对基础数据源进行更改。 **adLockOptimistic**或**adLockPessimistic**指定即时模式下，虽然**adLockBatchOptimistic**指定批处理模式。 **CursorLocation**属性可能会影响其**LockType**设置才可用。 例如， **adLockPessimistic**如果不支持设置**CursorLocation**属性设置为**adUseClient**。  
  
 在即时模式下，每次调用**更新**方法更改传播到数据源。 在批处理模式下，每次调用**更新**或移动的当前行位置将所做的更改保存到复制缓冲区，但仅**UpdateBatch**方法更改传播到数据源。  
  
 本部分包含以下主题。  
  
-   [更新数据](../../../ado/guide/data/updating-data.md)  
  
-   [保留数据](../../../ado/guide/data/persisting-data.md)
