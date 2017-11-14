---
title: "使用页 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34361d01b914d68cba1ff1e0e0f9378baf035be5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="using-pages"></a>使用页
使用**PageCount**属性来确定多少页的数据位于**记录集**对象。 *页*是一组记录其大小等于**PageSize**属性设置。 即使的最后一页是不完整，因为有较少的记录，比**PageSize**值，它将计为中的其他页**PageCount**值。 如果**记录集**对象不支持此属性， **PageCount**将为-1，则指示**PageCount**是无法确定。  
  
 使用**PageSize**属性来确定多少条记录组成的数据的逻辑页。 建立的页大小，可使用**AbsolutePage**属性可以移到特定页的第一个记录。 当你想要允许用户逐页浏览数据，一次查看一定数量的记录时，这是 Web 服务器方案中十分有用。  
  
 可以在任何时候，设置此属性，其值将用于计算的特定页的第一个记录的位置。  
  
 使用**AbsolutePage**属性来标识当前记录所在的页号。 同样，该提供程序必须支持相应的功能，此属性才可用。  
  
 **AbsolutePage**是基于 1 的并且等于 1 时的当前记录是中的第一个记录**记录集**。 设置此属性将移到特定页的第一个记录。 获取从页总数**PageCount**属性。

