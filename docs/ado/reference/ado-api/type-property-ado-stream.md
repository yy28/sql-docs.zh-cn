---
description: Type 属性（ADO 流）
title: " (ADO Stream) 类型属性 |Microsoft Docs"
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Type
- _Stream::get_Type
- _Stream::put_Type
helpviewer_keywords:
- Type property [ADO Stream]
ms.assetid: f6a17e8c-7a28-48d0-bded-76b9e0cf7639
author: rothja
ms.author: jroth
ms.openlocfilehash: 8fd1519092d72f8a562bb266d2aa6d547d8e37df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441729"
---
# <a name="type-property-ado-stream"></a>Type 属性（ADO 流）
指示 [流](../../../ado/reference/ado-api/stream-object-ado.md) 中包含的数据的类型 (二进制或文本) 。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 [StreamTypeEnum](../../../ado/reference/ado-api/streamtypeenum.md) 值，该值指定 **流** 对象中包含的数据的类型。 默认值为 **adTypeText**。 但是，如果二进制数据最初写入新的空 **流**，则该 **类型** 将更改为 **adTypeBinary**。  
  
## <a name="remarks"></a>备注  
 仅当当前位置在**流**的开头时， **Type**属性才是可读/写的 ([位置](../../../ado/reference/ado-api/position-property-ado.md)是 0) ，而在任何其他位置则为只读。  
  
 **Type**属性确定应该使用哪些方法来读取和写入**流**。 对于文本 **流**，请使用 [ReadText](../../../ado/reference/ado-api/readtext-method.md) 和 [WriteText](../../../ado/reference/ado-api/writetext-method.md)。 对于二进制 **流**，请使用 [读取](../../../ado/reference/ado-api/read-method.md) 和 [写入](../../../ado/reference/ado-api/write-method.md)。  
  
## <a name="applies-to"></a>适用于  
 [流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [RecordType 属性 (ADO) ](../../../ado/reference/ado-api/recordtype-property-ado.md)   
 [Type 属性 (ADO)](../../../ado/reference/ado-api/type-property-ado.md)
