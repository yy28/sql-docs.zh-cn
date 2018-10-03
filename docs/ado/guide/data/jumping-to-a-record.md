---
title: 跳转到一条记录 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7185dca3db146e7c17f41cb0f0c5376274fe3634
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747861"
---
# <a name="jumping-to-a-record"></a>跳转到记录
[移动](../../../ado/reference/ado-api/move-method-ado.md)方法，可在向前或向后移动**记录集**指定的数目的记录通过使用以下语法：  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>备注  
 **移动**方法支持对所有**记录集**对象。  
  
 如果*NumRecords*参数为大于零，将当前记录的位置向前移动 (年底**记录集**)。 如果*NumRecords*小于零，将当前记录位置向后移动 (的开头**记录集**)。  
  
 如果**移动**调用会将当前记录位置移动到之前的第一个记录点，ADO 将当前记录设置为中的第一个记录之前的位置**记录集**(**BOF**是**True**)。 试图移动时，向后**BOF**属性已**True**生成一个错误。  
  
 如果**移动**调用会将当前记录位置移动到点，在最后一条记录后，ADO 的位置后的最后一个记录集的当前记录**记录集**(**EOF**是**True**)。 试图移动时，向前**EOF**属性已**True**生成一个错误。  
  
 调用**移动**方法从一个空**记录集**对象生成一个错误。  
  
 如果通过中的书签*启动*参数，与此书签的记录在移动假设**记录集**对象支持书签。 通过使用获取书签[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)属性。 如果未指定，移动是相对于当前记录。  
  
 如果使用的**CacheSize**属性以在本地缓存从提供程序，记录传递*NumRecords*移动缓存记录的当前组之外的当前记录位置的参数强制 ADO 要检索的记录，从目标记录开始新的组。 **CacheSize**属性确定新检索组的大小和目标记录是检索到的第一个记录。
