---
description: 过程集合 (ADOX)
title: 过程集合 (ADOX) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Procedures
- Catalog::Procedures
helpviewer_keywords:
- Procedures collection [ADOX]
ms.assetid: dc7a38e1-93b9-4034-9af2-ff419e8fb2a3
author: rothja
ms.author: jroth
ms.openlocfilehash: 3719107d002e91880d59b0ba33c25c09596a80b9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439619"
---
# <a name="procedures-collection-adox"></a>过程集合 (ADOX)
包含目录的所有 [过程](../../../ado/reference/adox-api/procedure-object-adox.md) 对象。  
  
## <a name="remarks"></a>备注  
 **过程**集合的[APPEND](../../../ado/reference/adox-api/append-method-adox-procedures.md)方法对于 ADOX 是唯一的。 可以：  
  
-   使用 **Append** 方法向集合中添加一个新过程。  
  
 其余属性和方法对于 ADO 集合是标准的。 可以：  
  
-   使用 [Item](../../../ado/reference/ado-api/item-property-ado.md) 属性访问集合中的过程。  
  
-   返回集合中包含 [Count](../../../ado/reference/ado-api/count-property-ado.md) 属性的过程数。  
  
-   使用 [Delete](../../../ado/reference/adox-api/delete-method-adox-collections.md) 方法从集合中删除过程。  
  
-   更新集合中的对象，以反映包含 [Refresh](../../../ado/reference/ado-api/refresh-method-ado.md) 方法的当前数据库架构。  
  
 本部分包含以下主题。  
  
-   [索引集合属性、方法和事件](../../../ado/reference/adox-api/indexes-collection-properties-methods-and-events.md)  
  
## <a name="see-also"></a>另请参阅  
 [Command 和 CommandText 属性示例 (VB) ](../../../ado/reference/adox-api/command-and-commandtext-properties-example-vb.md)   
 [参数集合、Command 属性示例 (VB) ](../../../ado/reference/adox-api/parameters-collection-command-property-example-vb.md)   
 [步骤 Append 方法示例 (VB) ](../../../ado/reference/adox-api/procedures-append-method-example-vb.md)   
 [过程 Delete 方法示例 (VB) ](../../../ado/reference/adox-api/procedures-delete-method-example-vb.md)   
 [过程 Refresh 方法示例 (VB) ](../../../ado/reference/adox-api/procedures-refresh-method-example-vb.md)   
 [过程集合属性、方法和事件](../../../ado/reference/adox-api/procedures-collection-properties-methods-and-events.md)   
 [目录对象 (ADOX) ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [过程对象 (ADOX)](../../../ado/reference/adox-api/procedure-object-adox.md)
