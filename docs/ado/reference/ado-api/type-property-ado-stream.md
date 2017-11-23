---
title: "类型属性 （ADO 流） |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords: Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 326dfd1e359d28188a41d45c0054a082a9a69515
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="type-property-ado-stream"></a>类型属性 （ADO 流）
指示数据中包含的类型[流](../../../ado/reference/ado-api/stream-object-ado.md)（二进制或文本）。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回[StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md)值，该值指定中包含的数据类型**流**对象。 默认值是**adTypeText**。 但是，如果二进制数据最初编写为一个新的则为空**流**、**类型**将更改为**adTypeBinary**。  
  
## <a name="remarks"></a>注释  
 **类型**属性为读/写，仅当当前的位置的开头时，才**流**([位置](../../../ado/reference/ado-api/position-property-ado.md)为 0)，并在任何其他位置以只读的。  
  
 **类型**属性确定应使用哪些方法来进行读取和写入**流**。 文本**流**，使用[ReadText](../../../ado/reference/ado-api/readtext-method.md)和[WriteText](../../../ado/reference/ado-api/writetext-method.md)。 为二进制文件**流**，使用[读取](../../../ado/reference/ado-api/read-method.md)和[编写](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>适用范围  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [RecordType 属性 (ADO)](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 属性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
