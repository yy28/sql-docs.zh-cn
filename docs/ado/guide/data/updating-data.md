---
title: 更新数据 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bd3b72e897b8ae12441c7cf28d1995eb45318d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923695"
---
# <a name="updating-data"></a>更新数据
更新行为和功能在很大程度上取决于更新模式（锁定类型）、游标类型和游标位置。  
  
 使用**Update**方法可以保存对**记录集**对象的当前记录所做的任何更改，因为调用了**AddNew**方法或更改了现有记录中的任何字段值。 **Recordset**对象必须支持更新。  
  
 如果**Recordset**对象支持批处理更新，则可以在调用**UpdateBatch**方法之前，将多个更改缓存到本地一个或多个记录。 如果在调用**UpdateBatch**方法时编辑当前记录或添加新记录，ADO 将自动调用**Update**方法，以便在将批处理更改传输到提供程序之前保存当前记录的所有挂起的更改。  
  
 调用**Update**或**UpdateBatch**方法之后，当前记录保持最新。  
  
 本部分包含下列主题。  
  
-   [即时模式](../../../ado/guide/data/immediate-mode.md)  
  
-   [批处理模式](../../../ado/guide/data/batch-mode.md)  
  
-   [事务处理](../../../ado/guide/data/transaction-processing.md)
