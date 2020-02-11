---
title: 键集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Keys
- Keys
helpviewer_keywords:
- Keys collection [ADOX]
ms.assetid: cdb31c76-e559-475c-b33a-aac24f73e70e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a84932192fc7f51f21a7fd65c06c7417ef02da92
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67965838"
---
# <a name="keys-collection-adox"></a>项集合 (ADOX)
包含[表](../../../ado/reference/adox-api/table-object-adox.md)的所有[关键](../../../ado/reference/adox-api/key-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 [键集合](../../../ado/reference/adox-api/keys-collection-adox.md)的[APPEND](../../../ado/reference/adox-api/append-method-adox-keys.md)方法对于 ADOX 是唯一的。 可以：  
  
-   使用[Append](../../../ado/reference/adox-api/append-method-adox-keys.md)方法向集合中添加一个新项。  
  
 其余属性和方法对于 ADO 集合是标准的。 可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)属性访问集合中的键。  
  
-   返回具有[Count](../../../ado/reference/ado-api/count-property-ado.md)属性的集合中包含的键的数目。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法从集合中删除键。  
  
-   更新集合中的对象，以反映包含[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法的当前数据库的架构。  
  
 本部分包含以下主题。  
  
-   [索引集合属性、方法和事件](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule 属性示例（VB）](../../../ado/reference/adox-api/keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [键集合属性、方法和事件](../../../ado/reference/adox-api/keys-collection-properties-methods-and-events.md)   
 [项对象 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)
