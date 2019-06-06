---
title: 使用页 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6afd68ddf99799288939eeb0c6522275ec4d273f
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704536"
---
# <a name="using-pages"></a>使用页
使用**PageCount**属性来确定多少页的数据位于**记录集**对象。 *页面*是一组记录的大小等于**PageSize**属性设置。 即使最后一页是不完整，因为有比记录更少**PageSize**值，它计为中的其他页**PageCount**值。 如果**记录集**对象不支持此属性，请**PageCount**将为-1 指示**PageCount**是无法确定。  
  
 使用**PageSize**属性来确定多少条记录组成的数据的逻辑页。 建立页面大小，可使用**AbsolutePage**属性将移动到特定页面的第一个记录。 当你想要允许用户逐页浏览数据，一次查看特定数量的记录时，这是在 Web 服务器方案中有用。  
  
 可以在任何时候，设置此属性，其值将用于计算某一特定页的第一个记录的位置。  
  
 使用**AbsolutePage**属性标识的当前记录所在的页号。 同样，提供程序必须支持相应的功能，此属性才可用。  
  
 **AbsolutePage**是基于 1 的和等于 1 时的当前记录中的第一个记录**记录集**。 设置此属性将移动到特定页面的第一个记录。 获取从总页数**PageCount**属性。
