---
title: 跳转到记录 |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4da5573ef2f96947f9d8660d8d3461df879398e4
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35272026"
---
# <a name="jumping-to-a-record"></a>跳转到一条记录
[移动](../../../ado/reference/ado-api/move-method-ado.md)方法允许您在向前或向后移动**记录集**指定的数目的记录通过使用以下语法：  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>Remarks  
 **移动**方法支持对所有**记录集**对象。  
  
 如果*NumRecords*参数为大于零，将当前记录的位置前移 (的一端**记录集**)。 如果*NumRecords*小于零，将当前记录的位置向后移动 (右边的开头**记录集**)。  
  
 如果**移动**调用会将当前记录位置移动到前面第一条记录的某个点，ADO 将当前记录设置为之前的第一个记录的位置**记录集**(**BOF**是**True**)。 试图移动向后在**BOF**属性已**True**生成错误。  
  
 如果**移动**调用会将当前记录位置移动到点，在最后一条记录后，ADO 后的最新记录将当前记录设置为位置**记录集**(**EOF**是**True**)。 试图移动向前在**EOF**属性已**True**生成错误。  
  
 调用**移动**方法从一个空**记录集**对象生成一个错误。  
  
 如果通过中的书签*启动*相对于与此书签记录的自变量，移动是假定**记录集**对象支持书签。 使用获取书签[书签](../../../ado/reference/ado-api/bookmark-property-ado.md)属性。 如果未指定，移动是相对于当前记录。  
  
 如果你使用**CacheSize**属性以在本地传递缓存提供程序，从记录*NumRecords*缓存记录的当前组之外记录的当前位置移的自变量强制 ADO 检索的记录，从目标记录开始新的组。 **CacheSize**属性确定新检索到的组中的大小和目标记录是检索的第一个记录。
