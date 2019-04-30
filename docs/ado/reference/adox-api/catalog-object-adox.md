---
title: 目录对象 (ADOX) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5547090443e2f22a135234853b76480fb8295e14
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184210"
---
# <a name="catalog-object-adox"></a>目录对象 (ADOX)
包含集合 ([表](../../../ado/reference/adox-api/tables-collection-adox.md)，[视图](../../../ado/reference/adox-api/views-collection-adox.md)，[用户](../../../ado/reference/adox-api/users-collection-adox.md)，[组](../../../ado/reference/adox-api/groups-collection-adox.md)，并[过程](../../../ado/reference/adox-api/procedures-collection-adox.md))，描述的架构目录中的数据源。  
  
## <a name="remarks"></a>备注  
 您可以修改**目录**对象通过添加或删除对象或通过修改现有对象。 某些提供程序可能不支持的所有**目录**对象，或在仅支持查看架构信息。  
  
 使用的属性和方法**目录**对象，你可以：  
  
-   通过设置打开目录[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)属性设置为 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象或有效的连接字符串。  
  
-   创建一个新目录，附带[创建](../../../ado/reference/adox-api/create-method-adox.md)方法。  
  
-   确定中对象的所有者**目录**与[GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md)并[SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)方法。  
  
 本部分包含以下主题。  
  
-   [目录对象属性、方法和事件](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>请参阅  
 [目录 ActiveConnection 属性示例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Command 和 CommandText 属性示例 (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [连接的 Close 方法、 表 Type 属性示例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create 方法示例 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [项 Append 方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [参数集合、 Command 属性示例 (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [过程 Append 方法示例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [过程 Delete 方法示例 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [过程 Refresh 方法示例 (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [视图和字段集合示例 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [视图 Append 方法示例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [视图集合、 CommandText 属性示例 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [视图 Delete 方法示例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [视图 Refresh 方法示例 (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
