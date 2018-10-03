---
title: 字段相关错误信息 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- field-related errors [ADO]
- errors [ADO], field-related
ms.assetid: 5e7b1af4-996b-47c5-9161-c5575ad4fec9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 01f456527d7be8a954fecdace730bd1f8e47936b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47813045"
---
# <a name="field-related-error-information"></a>字段相关错误信息
如果字段直接与错误 — 例如，如果缺少数据或它的类型有误的字段 — 可以通过检查来检索有关原因的问题的详细信息**字段**对象的**状态**属性。 此属性已得到增强，提供有关该问题的特定信息。 因此，举例来说，在调用**UpdateBatch**可以通过查看来确定失败，问题的原因**状态**属性**字段**中每个受影响记录。 该属性将包含中的值之一**FieldStatusEnum**常量。 下表包含发生错误时特定的感兴趣的是这些值。  
  
|常量|ReplTest1|Description|  
|--------------|-----------|-----------------|  
|**adFieldCantConvertValue**|2|指示该字段不能检索或存储而不丢失数据。|  
|**adFieldDataOverflow**|6|指示提供程序返回的数据溢出字段的数据类型。|  
|**adFieldDefault**|13|指示该字段的默认值已设置数据时使用。|  
|**adFieldIgnore**|15|指示在源中设置数据值时跳过此字段。 提供程序不设置任何值。|  
|**adFieldIntegrityViolation**|10|指示不能修改该字段，因为它是计算或派生的实体。|  
|**adFieldIsNull**|3|指示提供程序返回一个 null 值。|  
|**adFieldOutOfSpace**|22|指示提供程序无法获取足够的存储空间来完成移动或复制操作。|
