---
title: ADOX 枚举常量 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- enumerated constants [ADOX]
ms.assetid: 9d91f511-d46f-44ef-97ef-77bf93836186
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f8c8fdcbbaab14a09114a435895a0ef2a2b79757
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="adox-enumerated-constants"></a>ADOX 枚举常量
若要帮助调试，ADOX 枚举常量，请列出每个常量的值。 但是，此值是纯粹是参考性的并且可以将不同的 ADOX 版本更改为另一个。 你的代码应仅依赖于的名称，而不是实际值的枚举常数。  
  
 定义以下枚举的常量。  
  
|枚举|Description|  
|-----------------|-----------------|  
|[ActionEnum](../../../ado/reference/adox-api/actionenum.md)|指定的类型时要执行操作**SetPermissions**调用。|  
|[AllowNullsEnum](../../../ado/reference/adox-api/allownullsenum.md)|指定是否具有 null 值的记录编制索引。|  
|[ColumnAttributesEnum](../../../ado/reference/adox-api/columnattributesenum.md)|指定的特征**列**。|  
|[DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md)|指定的数据类型**字段**，**参数**，或**属性**。|  
|[InheritTypeEnum](../../../ado/reference/adox-api/inherittypeenum.md)|指定对象如何继承权限集与**SetPermissions**。|  
|[KeyTypeEnum](../../../ado/reference/adox-api/keytypeenum.md)|指定的一种**密钥**： 主键、 外，或唯一。|  
|[ObjectTypeEnum](../../../ado/reference/adox-api/objecttypeenum.md)|指定为其设置权限或所有权的数据库对象的类型。|  
|[RightsEnum](../../../ado/reference/adox-api/rightsenum.md)|指定对某个对象的权限或组或用户的权限。|  
|[RuleEnum](../../../ado/reference/adox-api/ruleenum.md)|指定应时遵循的规则**密钥**被删除。|  
|[SortOrderEnum](../../../ado/reference/adox-api/sortorderenum.md)|指定索引列的排序顺序。|  
  
## <a name="see-also"></a>另请参阅  
 [ADOX API 参考](../../../ado/reference/adox-api/adox-api-reference.md)   
 [数据定义语言和安全性的 ADO 扩展 (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)
