---
description: 索引集合 (ADOX)
title: 索引集合 (ADOX) |Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 0075ca8340d869f803a10d296672e03326c5bad6
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770266"
---
# <a name="indexes-collection-adox"></a>索引集合 (ADOX)
包含表的所有 [索引](./index-object-adox.md) 对象。  
  
## <a name="remarks"></a>备注  
 **索引**集合的[APPEND](./append-method-adox-indexes.md)方法对于 ADOX 是唯一的。 方法：  
  
-   使用 **Append** 方法向集合中添加一个新索引。  
  
 其余属性和方法对于 ADO 集合是标准的。 方法：  
  
-   使用 [Item](../ado-api/item-property-ado.md) 属性访问集合中的索引。  
  
-   返回集合中包含 [Count](../ado-api/count-property-ado.md) 属性的索引数。  
  
-   使用 [Delete](./delete-method-adox-collections.md) 方法从集合中删除索引。  
  
-   更新集合中的对象，以反映包含 [Refresh](../ado-api/refresh-method-ado.md) 方法的当前数据库架构。  
  
 本部分包含以下主题。  
  
-   [索引集合属性、方法和事件](./indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [ (VB 的索引 Append 方法示例) ](./indexes-append-method-example-vb.md)   
 [索引对象 (ADOX)](./index-object-adox.md)