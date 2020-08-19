---
description: 目录对象 (ADOX)
title: " (ADOX) 的目录对象 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 35fa08ba0d93a7adacf6d58338f4808e2a5eba9e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88440379"
---
# <a name="catalog-object-adox"></a>目录对象 (ADOX)
包含描述数据源的架构目录)  ([表](../../../ado/reference/adox-api/tables-collection-adox.md)、 [视图](../../../ado/reference/adox-api/views-collection-adox.md)、 [用户](../../../ado/reference/adox-api/users-collection-adox.md)、 [组](../../../ado/reference/adox-api/groups-collection-adox.md)和 [过程](../../../ado/reference/adox-api/procedures-collection-adox.md) 的集合。  
  
## <a name="remarks"></a>备注  
 您可以通过添加或删除对象或通过修改现有对象来修改 **目录** 对象。 某些提供程序可能不支持所有 **目录** 对象，也可能只支持查看架构信息。  
  
 使用 **Catalog** 对象的属性和方法，你可以：  
  
-   通过将 [ActiveConnection](../../../ado/reference/adox-api/activeconnection-property-adox.md) 属性设置为 ADO [连接](../../../ado/reference/ado-api/connection-object-ado.md) 对象或有效的连接字符串，打开目录。  
  
-   使用 [create](../../../ado/reference/adox-api/create-method-adox.md) 方法创建新的目录。  
  
-   使用[GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md)和[SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md)方法确定**目录**中对象的所有者。  
  
 本部分包含以下主题。  
  
-   [目录对象属性、方法和事件](../../../ado/reference/adox-api/catalog-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [目录 ActiveConnection 属性示例 (VB) ](../../../ado/reference/adox-api/catalog-activeconnection-property-example-vb.md)   
 [Command 和 CommandText 属性示例 (VB) ](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [连接关闭方法，表类型属性示例 (VB) ](../../../ado/reference/adox-api/connection-close-method-table-type-property-example-vb.md)   
 [Create Method (VB) ](../../../ado/reference/adox-api/create-method-example-vb.md)   
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule Properties Example (VB) ](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [参数集合、Command 属性示例 (VB) ](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [ParentCatalog 属性示例 (VB) ](../../../ado/reference/adox-api/parentcatalog-property-example-vb.md)   
 [步骤 Append 方法示例 (VB) ](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [过程 Delete 方法示例 (VB) ](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [过程 Refresh 方法示例 (VB) ](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [视图和字段集合示例 (VB) ](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [ (VB) 视图追加方法示例 ](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 集合、CommandText 属性示例 (VB) ](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法示例 (VB) ](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [ (VB) Views Refresh 方法示例 ](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [组集合 (ADOX) ](../../../ado/reference/adox-api/groups-collection-adox.md)   
 [过程集合 (ADOX) ](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [表集合 (ADOX) ](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [用户集合 (ADOX) ](../../../ado/reference/adox-api/users-collection-adox.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
