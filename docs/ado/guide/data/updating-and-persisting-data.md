---
title: 更新和保留数据 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b251da97fe14abb8b10abe974c40b9adf0b37898
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699882"
---
# <a name="updating-and-persisting-data"></a>更新和保留数据
前面几章讨论了如何使用 ADO 来访问数据源中的数据、 如何在数据中，移动和了解如何编辑数据。 当然，如果你的应用程序的目标是允许用户对数据进行更改，您需要了解如何保存这些更改。 您也可以保留**记录集**更改为文件使用**保存**方法，或者可以发送所做的更改回存储使用的数据源**更新**或**UpdateBatch**方法。  
  
 在前面的章节中，更改的多个行中的数据**记录集**。 ADO 支持添加、 删除和修改的行的数据与相关的两个基本概念。  
  
 第一个概念是更改不会立即对**记录集**; 相反，因为它们由向内部*复制缓冲区*。 如果你决定不希望所做的更改，则放弃复制缓冲区中的修改。 如果您决定要保留更改，复制缓冲区中的更改应用于**记录集**。  
  
 第二个概念是，更改可以传播到数据源一旦您声明的行完成 (即*即时*模式)，或对一组行的所有更改将都回收，直至声明集的工作完成 (即*批处理*模式)。 **LockType**属性确定当对基础数据源进行更改。 **adLockOptimistic**或**adLockPessimistic**指定即时模式下，虽然**adLockBatchOptimistic**指定批处理模式。 **CursorLocation**属性可能会影响该**LockType**设置才可用。 例如， **adLockPessimistic**如果不支持设置**CursorLocation**属性设置为**adUseClient**。  
  
 在直接模式下，每次调用**更新**方法将更改传播到数据源。 在批处理模式下，每次调用**更新**或当前行位置的移动将所做的更改保存到复制缓冲区，但仅**UpdateBatch**方法将更改传播到数据源。  
  
 本部分包含以下主题。  
  
-   [更新数据](../../../ado/guide/data/updating-data.md)  
  
-   [保留数据](../../../ado/guide/data/persisting-data.md)
