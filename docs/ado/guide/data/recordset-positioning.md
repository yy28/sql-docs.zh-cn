---
title: 记录集定位 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f37f69b64e4a1a7fd55fb24a0c85d515971d4e72
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62910436"
---
# <a name="recordset-positioning"></a>记录集定位
使用**AbsolutePosition**属性将移动到一条记录，基于其序号位置**记录集**对象，或者想要确定当前记录的序号位置。 提供程序必须支持相应的功能，此属性才可用。  
  
 **AbsolutePosition**是基于 1 的和等于 1 时的当前记录中的第一个记录**记录集**。 正如前面提到的可以获取的中的记录总数**记录集**对象从**RecordCount**属性。  
  
 当您将设置**AbsolutePosition**属性，即使它是与当前缓存中的记录 ADO 重新加载缓存，通过从指定的记录的记录的新组。 **CacheSize**属性来确定此组的大小。  
  
> [!NOTE]
>  不应使用**AbsolutePosition**属性作为代理项记录号。 在给定的记录发生更改时删除前一条记录的位置。 此外没有给定的记录将具有相同不保证**AbsolutePosition**如果**记录集**重新查询对象或将其重新打开。 书签是推荐的方法来保留和返回到给定位置而且这是唯一的定位跨所有类型的方法**记录集**对象。
