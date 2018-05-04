---
title: 字段集合 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4eebfb3b3e401585829446872545063448ec87d6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="fields-collection-ado"></a>字段集合 (ADO)
包含所有[字段](../../../ado/reference/ado-api/field-object.md)的对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。  
  
## <a name="remarks"></a>注释  
 A**记录集**对象具有**字段**组成的集合**字段**对象。 每个**字段**对象中的列对应**记录集**。 你可以填充**字段**集合，然后再打开**记录集**通过调用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)对集合的方法。  
  
> [!NOTE]
>  请参阅**字段**对象主题有关的更多详细说明如何使用**字段**对象。  
  
 **字段**集合具有[追加](../../../ado/reference/ado-api/append-method-ado.md)方法，它临时创建并添加**字段**对象添加到收藏，和**更新**方法，完成任何添加或删除操作。  
  
 A**记录**对象具有可以使用编制索引的两个特殊字段[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)常量。 一个常量访问包含的默认流的字段**记录**，和其他访问包含的绝对 URL 字符串的字段**记录**。  
  
 某些提供程序 (例如， [Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) 可能填充**字段**有关可用字段的集合的子集**记录**或**记录集**。 直到它们被首先按名称引用或由你的代码编制索引，其他字段不添加到集合中。  
  
 如果你尝试按名称引用不存在的字段一个新**字段**对象将附加到**字段**具有集合[状态](../../../ado/reference/ado-api/status-property-ado-field.md)的**adFieldPendingInsert**。 当调用[更新](../../../ado/reference/ado-api/update-method.md)，ADO 将数据源中创建一个新域，如果你的提供程序允许的。  
  
 本部分包含以下主题。  
  
-   [字段集合属性、 方法和事件](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [字段对象](../../../ado/reference/ado-api/field-object.md)
