---
title: 索引集合（ADOX） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Table::Indexes
- Indexes
helpviewer_keywords:
- Indexes collection [ADOX]
ms.assetid: 184cf536-455c-42be-bf1c-a5c25bade961
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e84f49d5ad2d88ebb88417ae01046c0bcfd8006
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67966044"
---
# <a name="indexes-collection-adox"></a>索引集合 (ADOX)
包含表的所有[索引](../../../ado/reference/adox-api/index-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 **索引**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-indexes.md)方法对于 ADOX 是唯一的。 你可以：  
  
-   使用**Append**方法向集合中添加一个新索引。  
  
 其余属性和方法对于 ADO 集合是标准的。 你可以：  
  
-   使用[Item](../../../ado/reference/ado-api/item-property-ado.md)属性访问集合中的索引。  
  
-   返回集合中包含[Count](../../../ado/reference/ado-api/count-property-ado.md)属性的索引数。  
  
-   使用[Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法从集合中删除索引。  
  
-   更新集合中的对象，以反映包含[Refresh](../../../ado/reference/ado-api/refresh-method-ado.md)方法的当前数据库架构。  
  
 本部分包含以下主题。  
  
-   [索引集合属性、方法和事件](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [索引 Append 方法示例（VB）](../../../ado/reference/adox-api/indexes-append-method-example-vb.md)   
 [索引对象 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)
