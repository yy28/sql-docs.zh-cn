---
title: "目录对象 (ADOX) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
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
- Catalog
helpviewer_keywords:
- Catalog object [ADOX]
ms.assetid: bb651639-a488-4e38-b6de-0ed99fa4dd92
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26033bff0a1a88da25ed2eae566ffef49538c35f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="catalog-object-adox"></a>目录对象 (ADOX)
包含集合 ([表](../../../ado/reference/adox-api/tables-collection-adox.md)，[视图](../../../ado/reference/adox-api/views-collection-adox.md)，[用户](../../../ado/reference/adox-api/users-collection-adox.md)，[组](../../../ado/reference/adox-api/groups-collection-adox.md)，和[过程](../../../ado/reference/adox-api/procedures-collection-adox.md))，描述的架构目录中的数据源。  
  
## <a name="remarks"></a>注释  
 你可以修改**目录**通过添加或删除对象，或者通过修改现有对象的对象。 某些访问接口可能不支持的所有**目录**对象，或在仅支持查看架构信息。  
  
 使用的属性和方法**目录**对象，你可以：  
  
-   通过设置打开目录[ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md)属性 ADO[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象或有效的连接字符串。  
  
-   创建一个新目录，附带[创建](../../../ado/reference/adox-api/create-method-adox.md)方法。  
  
-   确定中的对象的所有者**目录**与[GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md)和[SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)方法。  
  
 本部分包含以下主题。  
  
-   [目录对象属性、 方法和事件](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录 ActiveConnection 属性示例 (VB)](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [命令和 CommandText 属性示例 (VB)](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [连接关闭方法，表类型的属性示例 (VB)](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [创建方法示例 (VB)](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [密钥追加方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [参数集合，命令属性示例 (VB)](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 属性示例 (VB)](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [过程追加方法示例 (VB)](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [过程删除方法示例 (VB)](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [过程刷新方法示例 (VB)](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [视图和字段集合示例 (VB)](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [视图追加方法示例 (VB)](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [视图集合，CommandText 属性示例 (VB)](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [视图删除方法示例 (VB)](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [视图刷新方法示例 (VB)](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [组集合 (ADOX)](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [过程集合 (ADOX)](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [用户集合 (ADOX)](../../../ado/reference/adox-api/users-collection-adox.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)

