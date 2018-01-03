---
title: "记录集定位 |Microsoft 文档"
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
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 28dcc44f38c763056a7a7f78979eee4f6de7df48
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="recordset-positioning"></a>记录集定位
使用**AbsolutePosition**属性可以移到一个记录，基于其序号位置**记录集**对象，或者想要确定当前记录的序号位置。 提供程序必须支持相应的功能，此属性才可用。  
  
 **AbsolutePosition**是基于 1 的并且等于 1 时的当前记录是中的第一个记录**记录集**。 如前所述，你可以获取的中的记录总数**记录集**对象**RecordCount**属性。  
  
 当你将设置**AbsolutePosition**属性，即使它是当前的缓存中中的记录 ADO 将重新加载缓存与新的组的开头你指定的记录的记录。 **CacheSize**属性确定此组的大小。  
  
> [!NOTE]
>  不应使用**AbsolutePosition**属性作为代理项记录号。 当删除前一条记录时，将更改给定的记录的位置。 此外没有给定的记录将具有相同不保证**AbsolutePosition**如果**记录集**重新查询对象或将其重新打开。 书签是推荐的方法来保留和返回到给定位置而且这是唯一的定位跨所有类型的方法**记录集**对象。
