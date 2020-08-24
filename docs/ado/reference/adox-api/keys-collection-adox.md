---
description: 项集合 (ADOX)
title: 项集合 (ADOX) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 95d1b5b927f03a0592f25cc4cc79c0ffe78cee74
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770056"
---
# <a name="keys-collection-adox"></a>项集合 (ADOX)
包含[表](./table-object-adox.md)的所有[关键](./key-object-adox.md)对象。  
  
## <a name="remarks"></a>备注  
 [键集合]()的[APPEND](./append-method-adox-keys.md)方法对于 ADOX 是唯一的。 方法：  
  
-   使用 [Append](./append-method-adox-keys.md) 方法向集合中添加一个新项。  
  
 其余属性和方法对于 ADO 集合是标准的。 方法：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 属性访问集合中的键。  
  
-   返回具有 [Count](../ado-api/count-property-ado.md) 属性的集合中包含的键的数目。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法从集合中删除键。  
  
-   更新集合中的对象，以反映包含 [Refresh](../ado-api/refresh-method-ado.md) 方法的当前数据库的架构。  
  
 本部分包含以下主题。  
  
-   [索引集合属性、方法和事件](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [键 Append 方法、Key Type、RelatedColumn、RelatedTable 和 UpdateRule Properties Example (VB) ](./keys-append-method-key-type-relatedcolumn-relatedtable-example-vb.md)   
 [键集合属性、方法和事件](./keys-collection-properties-methods-and-events.md)   
 [项对象 (ADOX)](./key-object-adox.md)