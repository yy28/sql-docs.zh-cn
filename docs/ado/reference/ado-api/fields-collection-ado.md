---
title: 字段集合 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Fields
- Recordset15::Fields
- _Record::Fields
helpviewer_keywords:
- Fields collection [ADO]
ms.assetid: 7c371474-b88f-4730-afa5-44163a0488d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74e6deb0caba88e6bbcf2897dcfa4aaaa22f04d0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63028234"
---
# <a name="fields-collection-ado"></a>字段集合 (ADO)
包含所有[字段](../../../ado/reference/ado-api/field-object.md)的对象[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)或[记录](../../../ado/reference/ado-api/record-object-ado.md)对象。  
  
## <a name="remarks"></a>备注  
 一个**记录集**对象具有**字段**组成的集合**字段**对象。 每个**字段**对象中的列对应**记录集**。 您可以填充**字段**集合，然后再打开**记录集**通过调用[刷新](../../../ado/reference/ado-api/refresh-method-ado.md)集合方法。  
  
> [!NOTE]
>  请参阅**字段**如何使用更多详细说明的主题**字段**对象。  
  
 **字段**集合中存在[追加](../../../ado/reference/ado-api/append-method-ado.md)方法，它会暂时将创建并添加**字段**到集合中，对象和一个**更新**方法，完成任何添加或删除操作。  
  
 一个**记录**对象具有可以使用索引的两个特殊字段[FieldEnum](../../../ado/reference/ado-api/fieldenum.md)常量。 一个常量访问包含的默认流的字段**记录**，和其他访问包含的绝对 URL 字符串的字段**记录**。  
  
 某些提供程序 (例如， [Microsoft OLE DB 访问接口用于 Internet 发布](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)) 可能会填充**字段**子集可用字段的集合**记录**或**记录集**。 其他字段不会添加到集合，直到它们被首次引用的名称或按你的代码索引。  
  
 如果你尝试按名称引用不存在的字段的新**字段**对象将附加到**字段**具有集合[状态](../../../ado/reference/ado-api/status-property-ado-field.md)的**adFieldPendingInsert**。 当您调用[更新](../../../ado/reference/ado-api/update-method.md)，ADO 将数据源中创建一个新域，如果您的提供程序允许。  
  
 本部分包含以下主题。  
  
-   [字段集合属性、 方法和事件](../../../ado/reference/ado-api/fields-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [字段对象](../../../ado/reference/ado-api/field-object.md)
