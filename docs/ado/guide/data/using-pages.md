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
author: rothja
ms.author: jroth
ms.openlocfilehash: 6542cb23deef9f10979e3bdb90c0820d84c0f150
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763028"
---
# <a name="using-pages"></a>使用页
使用**PageCount**属性来确定**记录集**对象中的数据页的数目。 *页面*是大小等于**PageSize**属性设置的记录组。 即使最后一个页面不完整，因为记录数少于**PageSize**值，也会在**PageCount**值中作为附加页面计数。 如果**记录集**对象不支持此属性，则**PageCount**将为-1，表示**PageCount**为无法确定。  
  
 使用**PageSize**属性来确定构成逻辑页数据的记录数。 通过建立页面大小，可以使用**AbsolutePage**属性移动到特定页面的第一条记录。 当你希望允许用户逐页浏览数据，一次查看一定数量的记录时，这非常有用。  
  
 此属性可随时设置，它的值将用于计算特定页面的第一条记录的位置。  
  
 使用**AbsolutePage**属性可以标识当前记录所在的页码。 同样，提供程序必须支持适当的功能，此属性才可用。  
  
 **AbsolutePage**从1开始，在当前记录是**记录集**的第一条记录时等于1。 设置此属性可以移动到特定页的第一条记录。 获取**PageCount**属性中的总页数。
