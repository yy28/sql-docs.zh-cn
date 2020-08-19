---
description: 视图集合 (ADOX)
title: Views 集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Catalog::Views
- Views
helpviewer_keywords:
- Views collection [ADOX]
ms.assetid: a55d380c-2b7b-4b57-af74-8ba0b3de0db9
author: rothja
ms.author: jroth
ms.openlocfilehash: aaf12e802e41b2dab638858eb2a08aacc3140ab6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439309"
---
# <a name="views-collection-adox"></a>视图集合 (ADOX)
包含目录的所有 [视图](../../../ado/reference/adox-api/view-object-adox.md) 对象。  
  
## <a name="remarks"></a>备注  
 **Views**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-views.md)方法对于 ADOX 是唯一的。 可以：  
  
-   使用 **Append** 方法将新视图添加到集合。  
  
 其余属性和方法对于 ADO 集合是标准的。 可以：  
  
-   使用 [Item](../../../ado/reference/ado-api/item-property-ado.md) 属性访问集合中的视图。  
  
-   返回集合中包含 [Count](../../../ado/reference/ado-api/count-property-ado.md) 属性的视图的数目。  
  
-   使用 [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 方法从集合中删除视图。  
  
-   更新集合中的对象，以反映包含 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法的当前数据库架构。  
  
 本部分包含以下主题。  
  
-   [视图集合属性、方法和事件](../../../ado/reference/adox-api/views-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [视图和字段集合示例 (VB) ](../../../ado/reference/adox-api/views-and-fields-collections-example-vb.md)   
 [ (VB) 视图追加方法示例 ](../../../ado/reference/adox-api/views-append-method-example-vb.md)   
 [Views 集合、CommandText 属性示例 (VB) ](../../../ado/reference/adox-api/views-collection-commandtext-property-example-vb.md)   
 [Views Delete 方法示例 (VB) ](../../../ado/reference/adox-api/views-delete-method-example-vb.md)   
 [ (VB) Views Refresh 方法示例 ](../../../ado/reference/adox-api/views-refresh-method-example-vb.md)   
 [目录对象 (ADOX) ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [视图对象 (ADOX)](../../../ado/reference/adox-api/view-object-adox.md)
