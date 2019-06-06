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
manager: jroth
ms.openlocfilehash: 8ea95b7d34f1395f6322d9a6ad6a0229bb8c7e45
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704569"
---
# <a name="updating-data"></a>更新数据
更新行为和功能是很大程度上取决于更新模式 （锁类型）、 游标类型和光标所在的位置。  
  
 使用**更新**方法以保存所做的当前记录的任何更改**记录集**对象调用以来**AddNew**方法或以来更改的任何字段值中的现有记录。 **记录集**对象必须支持更新。  
  
 如果**记录集**对象支持批量更新，你可以本地直到你调用缓存到一个或多个记录的多个更改**UpdateBatch**方法。 如果正在编辑当前记录或添加新记录，在调用时**UpdateBatch**方法，将自动调用 ADO**更新**方法将任何挂起的更改保存到之前的当前记录传输批的更改为提供程序。  
  
 当前记录保持最新调用后**更新**或**UpdateBatch**方法。  
  
 本部分包含以下主题。  
  
-   [即时模式](../../../ado/guide/data/immediate-mode.md)  
  
-   [批处理模式](../../../ado/guide/data/batch-mode.md)  
  
-   [事务处理](../../../ado/guide/data/transaction-processing.md)
