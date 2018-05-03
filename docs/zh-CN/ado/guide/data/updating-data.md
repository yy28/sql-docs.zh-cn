---
title: 更新数据 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc4f82996079bda6ba54f5329f8c78158677bc8d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data"></a>更新数据
更新行为和功能是很大程度上依赖于更新模式 （锁类型）、 游标类型和光标位置。  
  
 使用**更新**方法来保存到的当前记录所做的任何更改**记录集**以来调用的对象**AddNew**方法或以来更改的任何字段值中的现有记录。 **记录集**对象必须支持更新。  
  
 如果**记录集**对象支持批处理更新，你可以本地直到你调用缓存到一个或多个记录的多个更改**UpdateBatch**方法。 如果你要编辑的当前记录或添加一条新记录，当你调用**UpdateBatch**方法时，将自动调用 ADO**更新**方法将任何挂起的更改保存到之前的当前记录传输到提供程序的批处理的更改。  
  
 当前记录后，仍当前调用**更新**或**UpdateBatch**方法。  
  
 本部分包含以下主题。  
  
-   [即时模式](../../../ado/guide/data/immediate-mode.md)  
  
-   [批处理模式](../../../ado/guide/data/batch-mode.md)  
  
-   [事务处理](../../../ado/guide/data/transaction-processing.md)
