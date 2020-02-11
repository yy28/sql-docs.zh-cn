---
title: 目录对象（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9843ad9ac0a456f7e38e741e08ce9b66f862fd9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967052"
---
# <a name="catalog-object-adox"></a>目录对象 (ADOX)
包含描述数据源的架构目录的集合（[表](../../../ado/reference/adox-api/tables-collection-adox.md)、[视图](../../../ado/reference/adox-api/views-collection-adox.md)、[用户](../../../ado/reference/adox-api/users-collection-adox.md)、[组](../../../ado/reference/adox-api/groups-collection-adox.md)和[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)）。  
  
## <a name="remarks"></a>备注  
 您可以通过添加或删除对象或通过修改现有对象来修改**目录**对象。 某些提供程序可能不支持所有**目录**对象，也可能只支持查看架构信息。  
  
 使用**Catalog**对象的属性和方法，你可以：  
  
-   通过将[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)属性设置为 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象或有效的连接字符串，打开目录。  
  
-   使用[create](../../../ado/reference/adox-api/create-method-adox.md)方法创建新的目录。  
  
-   使用[GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md)和[SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)方法确定**目录**中对象的所有者。  
  
 本部分包含以下主题。  
  
-   [目录对象属性、方法和事件](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录 ActiveConnection 属性示例（VB）](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Command 和 CommandText 属性示例（VB）](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [连接关闭方法，表类型属性示例（VB）](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create 方法示例（VB）](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 属性示例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [Parameters 集合、Command 属性示例（VB）](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 属性示例（VB）](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [过程 Append 方法示例（VB）](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [过程 Delete 方法示例（VB）](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [过程 Refresh 方法示例（VB）](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [视图和字段集合示例（VB）](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [Views Append 方法示例（VB）](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 集合，CommandText 属性示例（VB）](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法示例（VB）](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [Views Refresh 方法示例（VB）](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [组集合（ADOX）](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [过程集合（ADOX）](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [表集合（ADOX）](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [用户集合（ADOX）](../../../ado/reference/adox-api/users-collection-adox.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
