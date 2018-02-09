---
title: "Size 属性 （ADO 流） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Size
helpviewer_keywords:
- Size property [ADO Stream]
ms.assetid: a487c241-d953-4c31-ae7e-6358d5cf6733
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cfd7bc505122ec142e61d53cdd3502c8c6ad3075
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="size-property-ado-stream"></a>Size 属性 （ADO 流）
指示流中的字节数的大小。  
  
## <a name="return-values"></a>返回值  
 返回**长**值，该值指定流的大小中的字节数。 如果流的大小未知，则默认值是流，则为-1 的大小。  
  
## <a name="remarks"></a>注释  
 **大小**可仅与打开[流](../../../ado/reference/ado-api/stream-object-ado.md)对象。  
  
> [!NOTE]
>  中可存储任意数量的位**流**对象，仅受系统资源限制。 如果**流**包含超出可由支持的位数**长**值，**大小**截断并因此不准确地表示的总**流**。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [Size 属性（ADO 参数）](../../../ado/reference/ado-api/size-property-ado-parameter.md)
