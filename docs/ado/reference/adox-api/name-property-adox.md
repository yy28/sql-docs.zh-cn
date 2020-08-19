---
description: Name 属性 (ADOX)
title: 名称属性 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Table::PutName
- _Table::GetName
- _Key::Name
- _Key::get_Name
- _Column::GetName
- _Index::Name
- _Index::put_Name
- _Column::PutName
- _Key::put_Name
- _Table::put_Name
- _User25::PutName
- _Index::get_Name
- _Column::get_Name
- _Group25::Name
- _Group25::get_Name
- _Column::Name
- _User25::get_Name
- _Table::Name
- _Group25::GetName
- _Index::PutName
- _Column::put_Name
- _Key::GetName
- _Table::get_Name
- _User25::Name
- _User25::put_Name
- _Index::GetName
- _User25::GetName
helpviewer_keywords:
- Name property [ADOX]
ms.assetid: 81b92baf-b6b9-4f4e-9f33-4503795518cd
author: rothja
ms.author: jroth
ms.openlocfilehash: dbd0d9088ea39d604c53c462448ae1c94b3a9052
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439779"
---
# <a name="name-property-adox"></a>Name 属性 (ADOX)
指示对象的名称。  
  
## <a name="settings-and-return-values"></a>设置和返回值  
 设置或返回一个 **字符串** 值。  
  
## <a name="remarks"></a>备注  
 名称在集合中不必是唯一的。  
  
 **Name**属性对[列](../../../ado/reference/adox-api/column-object-adox.md)、[组](../../../ado/reference/adox-api/group-object-adox.md)、[键](../../../ado/reference/adox-api/key-object-adox.md)、[索引](../../../ado/reference/adox-api/index-object-adox.md)、[表](../../../ado/reference/adox-api/table-object-adox.md)和[用户](../../../ado/reference/adox-api/user-object-adox.md)对象是可读/写的。 " **名称** " 属性在 " [目录](../../../ado/reference/adox-api/catalog-object-adox.md)"、" [过程](../../../ado/reference/adox-api/procedure-object-adox.md)" 和 " [视图](../../../ado/reference/adox-api/view-object-adox.md) " 对象上是只读的。  
  
 对于读/写对象 (**列**、 **组**、 **键**、 **索引**、 **表** 和 **用户** 对象) ，默认值为空字符串 ( "" ) 。  
  
> [!NOTE]
>  对于键，此属性在已追加到集合的 **键** 对象上是只读的。 对于表，对于已追加到集合的 **表** 对象，此属性是只读的。  
  
## <a name="applies-to"></a>适用于  

:::row:::
    :::column:::
        [列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)  
        [组对象 (ADOX)](../../../ado/reference/adox-api/group-object-adox.md)  
        [索引对象 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)  
    :::column-end:::
    :::column:::
        [项对象 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)  
        [过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)  
        [属性对象 (ADO)](../../../ado/reference/ado-api/property-object-ado.md)  
    :::column-end:::
    :::column:::
        [表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)  
        [用户对象 (ADOX)](../../../ado/reference/adox-api/user-object-adox.md)  
        [视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅  
 [列和表追加方法、Name 属性示例 (VB) ](../../../ado/reference/adox-api/columns-and-tables-append-methods-name-property-example-vb.md)   
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule Properties Example (VB) ](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)
